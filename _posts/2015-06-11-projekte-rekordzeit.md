---
layout: post
title: Endlich Stress! Projekte in Rekordzeit abschließen
categories: Programmierung
---
"Oh nein, schon wieder zu wenig Zeit!" - So oder so ähnlich sind die Gedanken eines Programmierers, wenn man ihm ein neues Projekt verkaufen will. Aber wie verhält sich eigentlich die Projektzeit zur tatsächlich benötigten Zeit? Und ist Stress wirklich so schlecht, wie immer behauptet wird?
<!--more-->
### Warum nicht jeder IT-Projekte schätzen kann

Wenn ein Programmierer Zeiten von seinem Vorgesetzten oder jemandem, der eher Management als Programmiererfahrungen hat einfach vorgesetzt bekommt, kann es wirklich sein, dass die Zeiten etwas zu knapp bemessen sind. Verschiedene Fallstricke, Inkompatiblitäten der Bibliotheken oder Plattformen und ähnliche Probleme können von einem "Laien" leider nur schlecht eingeschätzt werden. Funktionalitäten sehen oft sehr leicht zu implementieren aus, stellen sich aber bei der tatsächlichen Implementierung als absolutes Horrorszenario heraus. Fragt man stattdessen den Entwickler der die tatsächliche Umsetzung machen soll, wird die Zeit oft so großzügig abgeschätzt, dass zwar alle Eventualitäten irgendwie berücksichtigt sind - in der Regel sind die Projekte dann allerdings betriebswirtschaftlich nicht mehr lohnend. Aus diesem Grund ist weder das eine, noch das andere eine gute Idee. Im folgenden beschreibe ich noch zwei weitere Methoden der Projektzeitschätzung:

### Die 3 Zeiten Methode

Damit man die Bedürfnisse aller Parteien berücksichtigen kann, haben sich in den letzten Jahren verschiedene Methoden herauskristallisiert, die einer realistischen Schätzung näher kommen, als sich nur auf das Bauchgefühl zu verlassen. Die erste davon, ist die 3 Zeiten Methode (auch 3 Punkt Methode oder PERT-Schätzung genannt). Dabei geht man von den 3 Fällen aus, die eintreten können und errechnet daraus eine gewichtete Schätzung: Berücksichtigt wird der Best Case ("Schneller geht es nicht") + 4,  der Likey-Case ("Alles läuft glatt") und der Worst Case ("Absolut alles geht schief"). Danach teilt man die Zahl durch 6. Auf diesem Weg erhält man eine Schätzung, die den Best Case möglichst hoch gewichtet, die anderen Faktoren aber nicht außer Acht lässt.

### Probleme mit der 3 Zeiten Methode

Wie bereits beschrieben, wird mit der 3 Zeiten Methode der Best Case besonders stark gewichtet. Bereits Tom DeMarco, der auch als Begründer der strukturellen Analyse gilt hat festgestellt, dass die pessimistischen Werte deutlich häufiger auftreten, als die vorausgesagten Best Case Werte. Er verfeinerte daraufhin in seinem Buch "Bärentango"die Schätzungen mit eigener Methodik, um eine genauere Schätzung zu erzielen. Dennoch ist diese Methode der Zeitschätzung ziemlich ungenau und daher unter modernen Entwicklern nicht mehr sehr weit verbreitet.

### Die Scrum-Methode: Story-Points

Da Projekte häufig aus vielen Arbeitsschritten bestehen, besteht ein neuerer Ansatz um Zeiten zu schätzen darin, dass man Story Points statt statischen Zeitwerten dazu benutzt einzuschätzen, wie komplex eine bestimmte Funktionalität im Vergleich zu anderen Funktionalitäten aus dem selben Projekt sind. Auch hier werden gewichtetete Schätzungen vorgenommen, allerdings wird das gesamte Projektteam zur Einschätzung der Funktionalität befragt und damit eine deutlich genauere Einschätzung vorgenommen, als wenn nur eine Person alleine den Aufwand geschätzt hätte. Außerdem werden Story Points so verteilt, dass Sie mit der Größe der Komplexität immer höherwertig werden. Dafür wird zum Beispiel die Fibonacci-Reihe genommen um auszudrücken, dass j größer die Schätzung ist, desto höher die zu erwartende Ungenauigkeit sein wird. Weitere Informationen zum Thema Story Points findet man zum Beispiel auf der Seite von [Kai Simons](http://www.ksimons.de/2011/06/story-points-verstandlich-erklart/).

### Stress und das Parkinson'sche Gesetz

Wie auch immer die Zeitschätzung am Ende vorgenommen wird, gegen Ende der Projektzeit wird man unweigerlich an den Punkt kommen, an dem es hektisch wird: Die zur Verfügung stehende Zeit wird immer kürzer und die Aufgaben scheinen kein Ende zu nehmen. Jetzt ist Stress angesagt! Aus diesem Grund sollte sich der Smart Programmer immer das Parkinson'sche Gesetz vor Augen halten:

> > “Work expands so as to fill the time available for its completion.”
> 
> > „Arbeit dehnt sich in genau dem Maß aus, wie Zeit für ihre Erledigung zur Verfügung steht.“

Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Parkinsonsche_Gesetze) Umso mehr Zeit wir also haben, um eine Aufgabe zu Erledigen, umso mehr Zeit werden wir also auch darauf verwenden. Für den optimistischen Smart Programmer heißt das aber auch, dass umso weniger Zeit uns noch für die Aufgabe zur Verfügung steht, umso produktiver werden wir und umso schneller können wir eine bestimmte Aufgabe abschließen. Aus diesem Grund sollten wir also nicht an einem engen Zeitplan verzweifeln, sondern uns ganz im Gegenteil darauf freuen, dass wir in der kurzen Zeit die uns zur Verfügung steht, die größtmögliche Leistung bringen. Wir werden dafür sorgen, dass wir unter Stress [störungsfrei arbeiten](http://www.smart-programmer.de/produktiv-programmieren/) können, vollkommen fokussiert sind und die Aufgaben mit größtmöglicher Effizienz erledigen. Aus diesem Grund sollte ein Smart Programmer immer eine optimistische Schätzung der Projektarbeitszeit bevorzugen. Und falls man doch einmal in den Zeitpuffer hineinarbeitet, ist das kein Beinbruch: Zumindest hat man die beste Leistung erbracht, die man erbringen konnte.