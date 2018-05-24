---
layout: post
title: Testautomatisierung - Einsatz von Mocks
categories: Programmierung
---
Testautomatisierung: Einsatz von Mocks

In diesem Teil unserer [Artikelserie](../einfuehrung-software-qs) über Software Testing und Testautomatisierung befassen wir uns mit sogenannten Mocks. Was das ist und wie ihr sie richtig verwenden könnt, erfahrt ihr im folgenden Artikel.
<!--more-->
Warum braucht man Mocks – und was ist das eigentlich?!?
-------------------------------------------------------

Wenn man den Bereich Testautomatisierung einmal etwas genauer betrachtet, versucht man nach Möglichkeit einzelne Teile der Software ohne Nebeneffekte automatisiert testen zu lassen, damit die Ergebnisse eindeutiger werden. Nehmen wir als Beispiel eine Client-Server-Applikation die auf eine Datenbank zugreift: Wenn man vom Client aus Tests ausführt, könnte zum Beispiel der Server nicht antworten und damit das Testergebnis verändern. Schlimmer wäre aber, wenn Ressourcen die der Server benutzt - in unserem Beispiel die Datenbank - als Datenquelle nicht so reagieren, wie wir es vorhersehen. Aufgrund eines Verbindungsabbruchs könnte nur die Hälfte der Informationen ankommen oder jemand hat im Hintegrund die Tabellen geändert und wir bekommen ganz andere Ergebnisse, als wir sie erwarten. Vielleicht wollte ein findiger Admin die Datenbank auch kleiner machen und hat die Datenbank mit dem Namen „Test“ aus diesem Grund sogar ganz gedroppt. Für Das Testing unseres Clients ist das also ein Horrorszenario, da viele Abhängigkeiten mit einbezogen werden müssen. Aber auch wenn wir uns kleinere Teile unseres Programmes anschauen, können Probleme auftreten. Ein Beispiel ist, wenn wir Bibliotheken benutzen, die vielleicht aufgrund von Abhängigkeiten nicht mehr die richtigen Werte liefern oder ähnliches. Damit wir deterministische, also vorhersehbare Tests schreiben können, müssen wir also sicherstellen, dass unser Programm sich bei gleichen Eingaben immer gleich verhält. Und genau hier kommen sogenannte Mocks ins Spiel.

Der Einsatz von Mocks zur Testautomatisierung
---------------------------------------------

Der Name „Mocks“ kommt aus dem englischen, wobei das Wort „mocking“ vortäuschen bedeutet und ein „Mock“ eine Art Attrappe darstellt. In unserem Beispiel würde also unser Mock so tun, als wäre er der Server oder die Datenbank und vorhersehbare Ergebnisse liefern. Das kann im Bereich der Webentwicklung und REST-Services z.B. die Bereitstellung eines bestimmten JSON-Objektes sein. Aber auch feste Objekte mit Methoden, die immer ein bestimmtes Ergebnis zurückliefern wären denkbar. Nehmen wir also an, unser Client würde eine Abfrage zur Passwort-Authorisierung machen. Der Server würde die Datenbank nach einem bestimmten Passworthash (nebst Salt, wir schreiben doch sichere Software ;-) ) fragen, den Passworthash des Clients errechnen und schauen, ob die beiden matchen. Damit man sich den Weg über den Server und die Datenbank spart ist es nun denkbar, dass unser Mock-Service einfach die gleiche Methode bereitstellt, wie die, die der Client benutzt um den Server nach Richtigkeit des Passworts zu fragen. Diese könnte dann einen bestimmten, vorher bekannten Hash gegen den hereingegebenen Wert prüfen, sodass „unsersicheresPasswort!1elf“ in unserem Unit-Test immer valide ist und alle anderen nicht. Und schon erreichen wir immer vorhersehbare Ergebnisse: **„ unsersicheresPasswort!1elf“ gibt immer true zurück, alles andere false!** Dasselbe kann man auch mit Objekten machen, die andere Objekte z.B. über Dependency Injection hereingereicht bekommen: Wir geben statt der Bibliothek xy unser Mock-Objekt rein, dass bei der Methode sum(x,y) immer die Summe von x und y zurückgibt und damit nachvollziehbar und ohne Seiteneffekte wird.

### 10 Einsatzgebiete für Mocks in der Testautomatisierung

1.  Mocking von Services (z.B. RESTFull-Services)
2.  Mocking von Datenquellen (z.B. Datenbanken)
3.  Mocking von Objektenproperties (z.B. fest eingecodet, dass Age immer 20 ist)
4.  Mocking von Objektmethoden (z.B. zur Ablösung von Bibliotheken in eine vereinfachte Variante)
5.  Mocking von Fehlern (z.B. werfen einer Network-Exception, die man sonst schwer erzeugen kann)
6.  Mocking von Benutzereingaben (z.B. die Annahme, dass der User böse Zeichen eingegeben hat)
7.  Mocking von Zuständen (z.B. Daten wurden gelöscht oder geändert, obwohl die eigentliche Datenquelle nicht angetastet wird
8.  Mocking von Zeitabständen (z.B. simulation einer sehr langsam antwortenden Applikation durch Einsattz von Sleep())
9.  Mocking von nicht-Existenten Dateien
10.  Mocking von nicht-existenten Netzwerkressourcen

### Mocking während der Entwicklung

Wenn man das Gebiet Testautomatisierung mal beiseite lässt, kann man durch Mocking auch schon während der Entwicklung seine Vorteile ziehen: So kann man beispielsweise simulieren, dass bestimmte Komponenten oder Services schon vorhanden sind, obwohl noch keine Zeile Code dafür geschrieben wurde. Auf diese Art kann man viel schneller Prototypen entwickeln, die dem User bereits zeigen, wie es einmal aussehen könnte, ohne dass man einen größeren Aufwand betreiben müsste.

Fazit
-----

Das Erstellen von Mocks ist sowohl im Bereich der Testautomatisierung als auch in der Entwicklung von unschätzbarem Wert. Aus diesem Grund sollte man sich als Smart Programmer immer fragen, ob man komplexe Anwendungssoftware wirklich immer am Stück entwickelt, oder an bestimmten Stellen mit Hilfe von Mocks einen großen Teil der Komplexität einfach simuliert, bis man die entsprechende Komponente wirklich umsetzt.