---
layout: post
title: Einführung in ORM (Object-Relational-Mapping)
categories: Programmierung
---
Viele Programmierer die regelmäßig mit Datenbanken im Business Umfeld zu tun haben, suchen einen einfachen Weg um sich die zum Teil lästige Arbeit mit SQL Queries zu ersparen. Aus diesem Grund werden häufig ORM-Frameworks benutzt, die das Programmierer-Leben einfacher machen können.  In diesem Artikel möchte ich euch die Grundlagen von ORM näher bringen.
<!--more-->
### Was ist eigentlich ORM?

Die Kurzform ORM steht für object-relational mapping (in Deutsch: Objektrelationale Abbildung) und versucht, die Daten aus Datenbanken direkt in die Objekte der jeweiligen Programmiersprache zu übersetzen. Dafür werden im .Net-Umfeld POCOs (Plain Old CLR Object), im Java-Umfeld POJOs (Plain Old Java Object) und in PHP POPOs (Plain Old PHP Object) genutzt. Diese Plain Old irgendwas Objects sind Objekte, die in der Regel nur Attribute und Get / Set-Methoden beinhalten. Sofern man ein ORM-Framework einsetzt, werden die Tabellenzeilen auf die jeweiligen Objekte und die Spalten der Tabellenzeile auf die Attribute abgebildet („Mapping“).

### Vorteile von ORM

Der Hauptvorteil von ORM liegt darin, dass man sich in einfachen Anwendungen nicht mit der Datenbank selbst befassen muss, sondern mit „normalen“ Objekten arbeiten kann. Um einen Wert zu ändern, ändert man einfach das Attribut des jeweiligen Objektes und sagt dem Framework, dass es nun den aktuellen Zustand des Objektes zurück in die Datenbank schreiben kann („persistieren“). Auf diese Weise kann man zum Beispiel seine GUI-Komponenten direkt an ein Objekt binden und braucht bei einem „Save“-Event keine SQL-Queries aus dem Objekt heraus zu erzeugen. Ein weiterer Vorteil der durch ORM entsteht, ist bedingt durch die starke Standardisierung der Datenhaltung: Da alles in Objektattributen gehalten wird, liegen die Daten immer in der gleichen Form vor. Auf diese Weise braucht ein ORM-Framework um mehrere Datenbanktypen zu unterstützen nur die entsprechenden Aktionen (hole Daten aus der DB ins Objekt,  schreibe Daten aus dem Objekt in die DB, ...) in dem jeweiligen Datenbankdialekt zu implementieren.

### Die Nachteile von ORM

ORM-Frameworks haben natürlich auch ein paar Nachteile, die ich niemandem verschweigen möchte: Zunächst einmal gibt es das Problem, dass die Datenbankstruktur bereits zur Implementierungszeit bekannt sein muss. Auch wenn viele denken mögen, dass man die Datenbankstruktur immer schon vorher kennt: Es gibt einige Programme, die dem User größtmögliche Flexibilität bei der Konfiguration lassen. So kann es sein, dass ein User sich zum Beispiel Formulare etc. zur Laufzeit zusammen konfigurieren kann. In diesem Fall kann das Datenbankmodell bis zur letzten Sekunde, nämlich wenn der User bereits mit der Applikation arbeitet, unbekannt sein. Weiterhin wird bei ORM-Frameworks eigentlich immer eine Art von Mapping benötigt: Man muss seinem Framework im Voraus sagen, welche Datenbanktabelle auf welches Plain old XY Object gemapped wird. Dazu gehört nicht nur, wie die Attribute heißen, sondern auch wie die Beziehungen der Tabellen untereinander sind, wie Namensstrategien für 1:n und n:m-Beziehungen funktionieren und im Zweifel sogar, wie Ids generiert werden. Als letztes sollte man sich noch bewusst machen, dass man durch den Einsatz von ORM-Frameworks nur bedingt Zugriff auf die generierten Queries hat: Wenn man eine etwas speziellere Abfrage braucht, kann es sein, dass man doch wieder auf SQL oder No-SQL-Befehle zurückgreifen muss (und damit die Datenbankunabhängigkeit verliert). In der Regel gibt es aber auch sogenannte "Inceptors", die es einem ermöglichen, die generierten Queries noch einmal kurz vor Ausführung zu manipulieren. Da die SQL-Queries in einer Blackbox automatisch generiert werden, können diese auch zu Performanceeinbußen führen.

### Fazit

Mit ein bisschen Konfigurationsaufwand und Einarbeitungszeit kann man mit ORM-Frameworks um einiges schneller programmieren: Da man direkt mit gewöhnlichen Objekten arbeitet, kann man seine Formulare etc. direkt über Databinding an die entsprechenden Objekte binden und spart sich das manuelle erstellen von Datenbank-Queries. Dennoch sollte man genau abschätzen, ob für das jeweilige Projekt der Einsatz des Frameworks Sinn macht. Der Overhead der durch den Einsatz entsteht, die Zeit die man zur Einarbeitung aufbringen muss und die eventuellen Performanceeinbußen sind nicht zu vernachlässigen und gerade bei kleineren Projekten zum Teil unverhältnismäßig.

### Auf einen Blick

#### Vorteile von ORM-Frameworks

*   Schnellere Programmierung durch Objektzugriffe statt Queries
*   Keine SQL- oder No-SQL Erstellung
*   Einfaches Handling
*   Datenbankunabhängigkeit (alle Datenbanken, die von dem ORM angesprochen werden können, können mit einem Code bedient werden)

#### Nachteile von ORM-Frameworks

*   Datenbankmodell muss zum Zeitpunkt der Mapping-Generierung bekannt sein
*   Man muss dem ORM-Framework "beibringen", wie es mit der Datenbank zu arbeiten hat (Mapping, Id-Generatorenstrategie,...)
*   Wenig Kontrolle über die generierten SQL- oder NoSQL-Statements
*   Performanceeinbußen und Overhead durch das Framework