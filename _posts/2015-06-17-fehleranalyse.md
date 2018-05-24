---
layout: post
title: Fehlersuche - 10 Tipps für schnellere Fehleranalyse
categories: Programmierung
---
"Hallo? Ich habe ein Problem!" Auch ein Smart Programmer kann Fehler nicht komplett vermeiden - egal wie gut die Qualitätssicherung ist. Um nicht zu viel Zeit mit der Fehlersuche zu verschwenden sollte man diese aber zumindest schnell eingrenzen können. Im folgenden findet Ihr 10 Tipps, wie man die Fehlersuche beschleunigen kann.
<!--more-->
1\. Informationen einholen und dokumentieren
--------------------------------------------

Egal welche Art von Fehler gemeldet wird - ein Smart Programmer dokumentiert den Fehler und die dazugehörige Lösung mit allen Informationen die er bekommen kann. Falls jemand anderes bei der Fehlersuche helfen muss, muss er nicht alle Informationen erneut anfragen und eine Knowledge Base zu bereits gelösten Fehlern kann sich als unbezahlbar herausstellen ("Das hatte ich schon mal, wie war das nochmal...?"). Aus diesem Grund ist irgendeine Form von Ticketsystem Pflicht, da man diese in der Regel gut filtern kann und die Fehlern bestimmten Versionsständen zuordnen kann. Auf diese Weise kann man auch feststellen, in welcher Version Fehler wieder aufgetreten sind und überprüfen, was bei dem entsprechenden Release falsch gelaufen ist.

2. Screenshots anfordern
------------------------

Ein Bild sagt mehr als tausend Worte. Wer kennt diese Bauernweisheit nicht? Und doch wird häufig viel Text hin und hergeschrieben, ohne das Problem in irgendeiner Form visuell dargestellt zu haben. Deshalb ist bei jeder Fehlersuche, bei der Userinteraktion eine Rolle spielt dringend angeraten, einen Screenshot anzufordern. Was uns direkt zum nächsten Punkt bringt.

3\. Versionsnummer gut sichtbar im Programm einblenden
------------------------------------------------------

Die tollsten Screenshots nützen einem nichts, wenn der Versionsstand auf dem man Fehlersuche betreibt nicht zu dem Versionsstand passt, der beim Kunden eingesetzt wird. Aus diesem Grund sollte die Versionsnummer des Programms mit allen Informationen (z.B. Server- und Clientversion) die zur Fehlersuche nötig sind so gut sichtbar angezeigt werden, dass sie auf jedem Screenshot sichtbar ist.

4\. Ausführliches Logging erleichtert die Fehlersuche
-----------------------------------------------------

Häufiger werde ich gefragt, was man denn eigentlich alles loggen soll. Wenn ich diese Frage höre antworte ich häufig "Alles" - nicht ohne ein schelmisches Grinsen. Natürlich macht es keinen Sinn, wenn jede Zeile einen eigenen Eintrag im Logfile bekommt, aber wenn man später Fehlersuche betreibt ist jede Information die man ohne nachzufragen erhält wirklich Gold (und Zeit) Wert. Aus diesem Grund kann man z.B. [Aspektorientierte Programmierung](http://www.smart-programmer.de/aspektorientierte-programmierung/) benutzen um Methoden ein- und Ausgänge zu überwachen, Aufrufe an externe Stellen (inkl. URL) wegloggen und weitere Informationen die einem schon bei der Dokumentation als nicht sofort durchschaubar auffallen beschreiben. Loglevel gibt es nicht ohne Grund!

5\. Tools zur Analyse von Logfiles benutzen
-------------------------------------------

Spätestens wenn die Logfiles zahlreicher werden und Informationen an vielen Stellen verstreut liegen lohnt es sich auf Tools zur Logfileanalyse zurückzugreifen (und damit ist nicht Notepad++ gemeint!). Verschiedene Freeware Tools wie zum Beispiel [Log Parser Lizard](http://www.lizard-labs.com/log_parser_lizard.aspx), [Log Parser Studio](http://blogs.technet.com/b/exchange/archive/2013/06/17/log-parser-studio-2-2-is-now-available.aspx) oder [Gamut Log Viewer](http://www.gamutsoftware.com/) lassen sich leicht über [Chocolatey](https://chocolatey.org/) installieren und bieten einem den Vorteil, Log Files in verschiedenen Formaten zu filtern oder sogar SQL-artige Queries darauf abzufeuern. Wenn man weiß wonach man sucht, kann dies bei der Fehlersuche eine unglaubliche Zeitersparnis sein!

6\. Fehler Nachstellen
----------------------

Im Zeitalter vom "Internet der Dinge" sind immer mehr Systeme untereinander gekoppelt und unterhalten sich miteinander. Aus diesem Grund wird die Fehlerkette immer größer und die Fehlerquelle kann sich auf verschiedene Ursachen verteilen. Deshalb ist es ungeheuer wichtig, Fehler die man nicht sofort lösen kann zunächst einmal selber nachzustellen. Nur auf diese Weise hat man Gelegenheit, ein genaueres Verständnis von den Ursachen zu erhalten oder bereits einige Punkte auszuschließen.

7\. Fehler genau verstehen
--------------------------

Wie häufig kommt es vor, dass beim nachstellen der Fehler einfach nicht vorhanden ist? Genau, sehr häufig! Aus diesem Grund ist es wichtig, genau zu verstehen welche Schritte unternommen wurden damit der Fehler auftritt und diese 1:1 nachzubilden. Die Fehlersuche ist häufig unproduktiv, weil der Programmierer und der Kunde aneinander vorbei reden. Ein Smart Programmer scheut deshalb auch nicht den telefonischen Kontakt zum Kunden, da 2 Minuten telefonieren und "es sich zeigen lassen" eine halbe Stunde Arbeit ersparen kann!

8\. Abhängigkeiten unabhängig voneinander testen
------------------------------------------------

Die Testumgebung ist aufgebaut, der Fehler ist reproduzierbar und trotzdem hat man keine Ahnung woher das Problem kommt - was könnte frustrierender sein? Spätestens an dieser Stelle macht es Sinn, die ganze Anwendung in seine Einzelteile zu zerlegen und die Fehlersuche auf einzelne Bereiche zu verlagern: Funktioniert die Datenbank? Dann testen wir sie nicht noch einmal, sondern benutzen ein Mock. Funktionieren die Bibliotheken einzeln? Super, dann benutzen wir auch hier ein Mock. Wenn der Fehler auftaucht, haben wir auf diese Weise bereits einige Punkte ausgeschlossen und können uns auf die verbleibenden Fehlerquellen konzentrieren.

9\. Testing automatisieren!
---------------------------

Wenn bei der Entwicklung schon keine Tests geschrieben wurden, macht es spätestens bei der Fehlersuche Sinn, Unit- und GUI Testautomatisierung zu betreiben. Auf diese Weise erspart man sich das wiederholte (und Fehleranfällige) Ausführen von Aktionen und sorgt dafür, dass dieser Bereich in Zukunft immer mit getestet wird.

10\. Keine falsche Eitelkeit: Um Hilfe Fragen!
----------------------------------------------

Als Faustregel sollte gelten, dass spätestens wenn man länger als eine halbe Stunde mit der Fehlersuche beschäftigt ist ein weiterer Kollege mit ins Boot geholt werden soll. Nicht nur das Fachwissen das zusätzlich mit einfließt ist hilfreich - oft reicht auch schon die Erklärung des Problems an eine andere Person für neue Denkansätze, auf die man "im Kopf" nicht gekommen wäre. Außerdem stellt sich nach einer Weile eine gewisse Blindheit gegenüber Fehlern ein, da das Gehirn gerne Informationen die ihm unwichtig erscheinen interpoliert. Deshalb kann es vorkommen, dass der Fehler die Ganze Zeit vor der eigenen Nase ist und man ihn trotzdem nicht sieht. Ein Smart Programmer kommt deshalb nicht in Versuchung aus falschem Stolz den Fehler selber zu lösen, sondern holt sich rechtzeitig Hilfe von einer weiteren Person.