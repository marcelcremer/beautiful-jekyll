---
layout: post
title: MSSQL Push Service
categories: Programmierung
---

Da ich von $Kunde die Anforderung bekommen habe, einen Datenbank-Push Service zu implementieren, habe ich mich eine Weile damit beschäftigt wie man am einfachsten einen entsprechenden MSSQL Push Service implementieren kann. <!--more-->Grundlage dafür sind bei mir verschiedene Trigger:

1.  Die „Notifier“ Trigger, so nenne ich sie mal, feuern nachdem ein Update oder ein Insert auf die zu überwachenden Tabellen durchgeführt wird. Diese füllen eine weitere Tabelle, eine Art Job-Queue mit Informationen über den Typ, woher getriggert wurde, wann getriggert wurde usw.. Das erleichtert das überwachen und ermöglicht es, Jobs die angefallen sind, während der Push-Empfänger nicht verfügbar war, später noch einmal auszuführen.
2.  Ein Trigger auf der Jobtabelle prüft, ob der Job der eingefügt wurde bereits an den Empfänger weitergeleitet wurde. Falls noch keine Weiterleitung erfolgt ist, ruft er eine Stored Procedure auf, die GeekZilla in seinem Blog am besten beschrieben hat:

Gefunden auf [Geekzilla](http://www.geekzilla.co.uk/View24CF9B2B-4099-4ED7-B360-89B14C11DAE8.htm)

CREATE PROCEDURE Http_request (@URI      VARCHAR(200), 
                               @response VARCHAR(8000) out) 
AS 
    DECLARE @xhr        INT, 
            @result     INT, 
            @httpStatus INT, 
            @msg        VARCHAR(255) 

    EXEC @result = Sp_oacreate 
      'MSXML2.XMLHttp.5.0', 
      @xhr out 

    IF @result <> 0 
      BEGIN 
          RAISERROR('sp_OACreate on MSXML2.XMLHttp.5.0 failed',16,1) 

          RETURN 
      END 

    EXEC @result = Sp_oamethod 
      @xhr, 
      'open', 
      NULL, 
      'GET', 
      @URI, 
      false 

    IF @result <> 0 
      BEGIN 
          RAISERROR('sp_OAMethod Open failed',16,1) 

          RETURN 
      END 

    EXEC @result = Sp_oamethod 
      @xhr, 
      send, 
      NULL, 
      '' 

    IF @result <> 0 
      BEGIN 
          RAISERROR('sp_OAMethod SEND failed',16,1) 

          RETURN 
      END 

    EXEC @result = Sp_oagetproperty 
      @xhr, 
      'status', 
      @httpStatus out 

    PRINT 'Status: ' 
          \+ CONVERT(VARCHAR(10), @httpStatus) 

    IF @result <> 0 
      BEGIN 
          RAISERROR('sp_OAMethod read status failed',16,1) 

          RETURN 
      END 

    IF @httpStatus <> 200 
      BEGIN 
          RAISERROR('sp_OAMethod http status bad',16,1) 

          RETURN 
      END 

    EXEC @result = Sp_oagetproperty 
      @xhr, 
      'responseText', 
      @response out 

    IF @result <> 0 
      BEGIN 
          RAISERROR('sp_OAMethod read response failed',16,1) 

          RETURN 
      END 

    EXEC @result = Sp_oadestroy 
      @xhr 

    RETURN 

go

Achtung: Was faktisch dabei passiert ist, dass ein COM-Object über eine DLL des IE aufgerufen wird, die die entsprechende Webseite aufruft. Ich habe das Ganze noch dahingehend modifiziert, dass eine ID mit übergeben wird, damit der Webservice direkt die ID bekommt, deren Job er abarbeiten muss.

1.  Ein Web-Service, in meinem Fall Javas REST-Implementierung Jersey nimmt die Anfrage entgegen, holt sich dann die Job-Informationen aus der DB und arbeitet das ganze entsprechend ab. Die Queue wird alle 15 Minuten auch noch einmal manuell durchlaufen, falls der REST-Service eine Anfrage nicht mitbekommen hat.

Alternativ hätte ich für den MSSQL Push Service auch eine CLR-Implementierung schreiben können, aber gefühlt wäre das zu viel Aufwand gewesen. (Korrigiert mich gerne, wenn dies falsch ist). Falls jemand mit dem Gedanken spielt, das ganze auszuprobieren folgender Hinweis: Die obige Implementierung benutzt die OLE-Funktionalität des MSSQL Servers, welche zunächst aktiviert werden muss. Außerdem müssen Sicherheitsrichtlinien angepasst werden, damit diese auch von einem Trigger ausgeführt werden dürfen. Da es sich in meinem Beispiel um eine Interne Datenbank handelt, auf die nicht von außen zugegriffen werden kann, hat sich der folgende Code dazu bewährt:

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OASetProperty\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OAMethod\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OAGetErrorInfo\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OADestroy\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OAStop\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OACreate\] TO \[public\]

GO

use \[master\]

GO

GRANT EXECUTE ON \[sys\].\[sp_OAGetProperty\] TO \[public\]

GO

sp_configure 'show advanced options', 1

GO

reconfigure

go

exec sp_configure

go

exec sp_configure 'Ole Automation Procedures', 1

\-\- Configuration option 'Ole Automation Procedures' changed from 0 to 1. Run the RECONFIGURE statement to install.

go

reconfigure

go

**Bei anderen Umgebungen muss darauf geachtet werden, ob die Sicherheitseinstellungen derart verändert werden dürfen!**