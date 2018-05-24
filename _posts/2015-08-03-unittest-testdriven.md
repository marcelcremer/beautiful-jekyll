---
layout: post
title: Unit Tests und Test Driven Development
categories: Programmierung
---
Im [ersten Teil unserer Artikelserie](../einfuehrung-software-qs) haben wir uns mit den verschiedenen Testmöglichkeiten von Software beschäftigt. In diesem Artikel gehe ich auf den Bereich Unit Tests und Test Driven Development ein.
<!--more-->
Warum braucht man Unit-Tests?
-----------------------------

Einzelne Teilbereiche komplexer Software sowie Software-Bibliotheken kann man sehr häufig mit Unit Tests automatisiert überprüfen lassen. Dafür muss man sicherstellen, dass einzelne Methoden oder Funktionen dem Prinzip der Single Responsibility - also jede Methode oder Funktion darf nur eine einzige Aufgabe übernehmen genügen. Wenn man dieses Prinzip erfüllt, kann man den Zweck der Methode genau beschreiben. Ein Beispiel:

function divide(a,b)
{
	if(isNaN(a) || isNaN(b))
		throw "Arguments need to be Numbers!";
	if(b == 0)
		throw "Division by zero is not allowed!";
	else
		return a / b;
}

In diesem Beispiel beschreiben wir eine einfache funktion, die 2 Zahlen dividiert. Damit diese Funktion ausgeführt werden kann, muss sowohl sichergestellt werden, dass wir nur Zahlen eingeben, als auch das wir nicht versuchen durch 0 zu teilen. Wenn wir nun die Funktionalität unserer Funktion sicherstellen möchten, würden wir manuell testen, indem wir die Funktion mit Grenzfällen "füttern":

*   Beide Parameter sind keine Zahl
*   Je ein Parameter ist keine Zahl
*   Beide Parameter sind 0
*   Je ein Parameter ist 0
*   Beide Parameter sind positive Ganzzahlen
*   Beide Parameter sind positive, rationale Zahlen
*   Beide Parameter sind negative Ganzzahlen
*   Beide Parameter sind negative, rationale Zahlen
*   Abwechselnde, rationale und Ganzzahlen der beiden Parameter

Damit hätten wir, wenn man mal die von der maximalen Zahlengröße absieht, alle Grenzfälle abgedeckt und könnten davon ausgehen, dass unsere Funktion in allen Fällen funktioniert. Theoretisch müsste man diese Tests bei jeder noch so kleinen Änderung wiederholen, denn es könnte sein, dass eine bestimmte  Kombination nach Anpassung des Codes nicht mehr funktioniert. Wir haben oben ein sehr triviales Beispiel gewählt. Standardapplikationen sind häufig noch um einiges komplexer. Um dieser Komplexität entgegen zu wirken und die Tests nicht immer alle manuell wiederholen zu müssen, kam jemand auf die Idee, auch die Tests zu programmieren. Diese Programme nennt man Unit Test.

Vor- und Nachteile von Unittests
--------------------------------

Unit Tests werden also geschrieben, um sich wiederholende Tests auf bestimmte Teilbereiche eines Programmes zu automatisieren. Dafür entwickelt man ein weiteres Programm, dass eine bestimmte Funktion mit Grenzfällen aufruft, damit diese abgedeckt sind und man auf diese Weise davon ausgehen kann, dass die Software funktioniert. Diese Vorgehensweise hat verschiedene Vor- und Nachteile.

### Vorteile von Unit Tests

*   Zeitersparnis durch automatisiertes Testing
*   Höhere Testabdeckung und erkennen von Seiteneffekten (häufig werden nur die geänderten Stellen der Software getestet und nicht, ob die weiteren Methoden auch noch funktionieren)
*   Erhöhung der Software Qualität
*   Integration in den [Build-Prozess](../build-prozess-automatisieren/) (Tests werden vor jeder Auslieferung durchgeführt)

Demgegenüber stehen natürlich auch ein paar Nachteile, die man leider nicht wegdiskutieren kann.

### Nachteile von Unit Tests

*   Zeitaufwand zum erstellen der Tests
*   Erkennen von Grenzfällen ist nicht immer trivial
*   Tests müssen, genau wie das Programm gewartet werden
*   Programmierfehler in Tests können falsche Sicherheit erwecken

Test Driven Development
-----------------------

Im Bereich der agilen Softwareentwicklung kam jemand auf die tolle Idee, dass es doch gut wäre, wenn die Tests programmiert werden würden, bevor man den eigentlichen Programmcode schreibt. In diesem Fall würden zunächst alle Tests fehlschlagen und wenn das Programm implementiert ist, würden die Tests nach und nach erfolgreich durchgeführt werden. Nach diesem Modell vorzugehen nennt man Test Driven Development. Die Vorteile liegen klar auf der Hand: Man muss sich zuerst darüber Gedanken machen, was genau man mit einem bestimmten Stück Code erreichen möchte und beginnt erst danach mit der eigentlichen Implementierung. Der Nachteil darin ist, dass man längere Zeit braucht, bis man erste Ergebnisse hat und das die Anforderungen oder die Grenzfälle nicht immer im Voraus abzuschätzen sind.

Fazit
-----

Sowohl Unit Tests als auch Test Driven Development sind durchaus Methoden, mit denen man die Softwarequalität verbessern kann. Man sollte an dieser Stelle jedoch nicht auf den allgemeinen Zug aufspringen und glauben, man habe den heiligen Gral der Softwareentwicklung entdeckt: Der Aufwand für Unit-Tests ist nicht nur, wie oft versprochen wird, ein einmaliger - auch Tests müssen gewartet und mit der Software weiter entwickelt werden. Und auch wenn alle Tests funktionieren und die einzelnen Komponenten gut mit Tests abgedeckt sind, heißt dies noch nicht, dass die Software insgesamt funktioniert. Aus diesem Grund sollte man genau überlegen, bei welchen Komponenten der zusätzliche Zeitaufwand für Unit Tests gerechtfertigt ist und ob dieser Zeitaufwand sich später wieder amortisiert. Aus diesem Grund gebe ich den Unit Tests 3 von 5 Sternen.