---
layout: post
title: MSSQL Constraints deaktivieren
categories: Kurz&Bündig
---

Durch eine aktuelle Anforderung musste ich Daten von einer Datenbank in eine andere Übernehmen. Störend ist dabei, wenn Constraints und Trigger einem die Show stehlen wollen und den Datenimport verhindern. <!--more-->Auf [StackOverflow](http://stackoverflow.com/questions/14972816/how-to-disable-constraints-for-all-the-tables-and-enable-it) habe ich dazu eine super Lösung gefunden. Mit den folgenden Befehlen kann man MSSQL Constraints deaktivieren. Außerdem werden die Trigger der Vollständigkeit halber temporär deaktiviert, sodass die Tabellen während des Imports davon nicht beeinflusst werden.

> EXEC sp_MSforeachtable @command1=”ALTER TABLE ? NOCHECK CONSTRAINT ALL” GO
> 
> EXEC sp_MSforeachtable @command1=”ALTER TABLE ? DISABLE TRIGGER ALL” GO
> 
> –Hier die INSERT INTO…SELECT einfügen
> 
> EXEC sp\_MSforeachtable @command1=”ALTER TABLE ? ENABLE TRIGGER ALL” GO EXEC sp\_MSforeachtable @command1=”ALTER TABLE ? CHECK CONSTRAINT ALL” GO

Der obige Code benutzt die undokumentierte sp_MSforeachtable-Methode des MSSQL Servers, der den danach folgenden Query für jede Tabelle ausführt (? wird durch Tabellenname ersetzt). Dadurch lassen sich schnell und einfach alle Constraints und Trigger für alle Tabellen einer Datenbank deaktivieren, die Daten übernehmen und danach wieder aktivieren. Was sonst noch stören kann, sind Identitity-Spalten, die keinen Insert erlauben (z.B. AutoWert-Spalten). Für diese Tabellen müssen jeweils noch ein

> SET IDENTITY_INSERT _<Tabellenname>_ on;

bzw. nach dem Befehl

> SET IDENTITY_INSERT _<Tabellenname>_ off;

eingefügt werden. Identity_insert kann übrigens nur für eine Tabelle Parallel aktiviert werden und ist nur in einer Session gültig, deshalb sollte man hier mit Batchverarbeitung (GO) arbeiten. Durch die Kombination, MSSQL Constraints deaktivieren und Identity/Trigger ignorieren kann man schnell und einfach Daten aus anderen Datenbanken und Tabellen in die entsprechenden Zieltabellen übernehmen.