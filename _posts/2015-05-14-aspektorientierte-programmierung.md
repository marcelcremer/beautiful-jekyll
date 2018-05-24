---
layout: post
title: Aspektorientierte Programmierung
categories: Programmierung
---

Die **aspektorientierte Programmierung** geht an vielen Programmierern leider immer noch vorbei. Dabei kann es in manchen Fällen besonders nützlich sein, wenn man zumindest weiß, was sich mit Aspekten in kurzer Zeit lösen lässt und wie man diese am besten einsetzt.
<!--more-->
### Aspektorientierte Programmierung: Die Grundbegriffe

Um eine grundsätzliche Idee zur aspektorientierten Programmierung zu bekommen, muss man zunächst einmal verstehen, wie diese grundsätzlich aufgebaut ist. Sie besteht aus 3 wesentlichen Komponenten:

1.  Bestimmte Stellen im Programm, sogenannte „_Join Points_“ dienen als eine Art Einfügepunkt für zusätzlichen  Code. Das Können zum Beispiel Methodenaufrufe oder das Verlassen von Methoden, Initialisierungen von Variablen und andere feste Punkte sein, die dafür verwendet werden, bestimmte Punkte fest zu definieren, in denen der zusätzliche Code eingefügt werden soll.
2.  An diesen „_Join Points_“ können nun sogenannte _„Advices“_ ausgeführt werden – das ist Code, der vor oder nach dem Erreichen des _Join Points_ eingefügt werden soll.
3.  Ein sogenannter „_Aspekt_“ fasst mehrere _„Advices“_ eines Programmes in sich zusammen, um die Übersichtlichkeit zu gewährleisten und die _„Advices“_ logisch zu ordnen.
4.  Die letzte wichtige Komponente, die für die Implementierung von aspektorientierter Programmierung wichtig ist, ist der sogenannte „Point cut“. Dieser gibt die Bedingung an, wann der _Aspekt_ in die entsprechenden Stellen eingefügt werden soll.

### Welche Vorteile hat die aspektorientierte Programmierung?

Nun, gehen wir mal davon aus, dass wir zum Beispiel alle Methoden, bei denen Werte verändert werden loggen wollen und zwar beim Eintritt in die Methode der Wert der hereingegeben wird und beim Austritt aus der Methode der veränderte Wert. Traditionellerweise würde man sich in jeder dieser Methoden einen Logger holen und die Werte von Hand beim Aufruf und vor Austritt aus der Methode herausloggen. Mittels der aspektorientierten Programmierung könnte man nun einen _Aspekt_ entwickeln, mit jeweils einem _Advice_ vor und einem nach dem Methodenaufruf, der die Werte ausgibt. Und diesen _Aspekt_ könnte man dann allen Methoden, die beispielsweise ein „set“, „calculate“ oder ähnliches im Namen haben via entsprechendem Point Cut anwenden. Damit würden alle Methoden gleich geloggt werden - und das unter Verwendung von nur einer einzigen Logging-Methode! Außerdem müsste man sich um das Problem nicht immer erneut kümmern, denn der Aspekt wird automatisch mit jedem erneuten Build in den vorhandenen Code „hineingewoben“.

### Für welche Programmiersprachen ist aspektorientierte Programmierung möglich?

Der bekannteste Vertreter für AOP ist die Aspectj für Java. Wer Java mit Eclipse entwickelt, hat auch eine vollständige Integration für Pointcuts etc., sodass an den entsprechenden Stellen ein „AJ“-Icon ähnlich dem Break-Point-Icon angezeigt wird und darauf hinweist, dass an dieser Stelle ein Aspect greift. Ähnliche Implementierungen gibt es auch für den .Net-Bereich, wie z.B. Aspect.Net oder Aspect#. Für andere Programmiersprachen kann ich nur empfehlen, eine gängige Suchmaschine für weitere Informationen zu konsultieren. Für Java Programmierer kann ich das Buch "Aspektorientierte Programmierung mit AspectJ 5: Einsteigen in AspectJ und AOP" als weitere Lektüre empfehlen. Nach einer kurzen Einführung in das Thema kommt der Autor Oliver Böhm sehr schnell zu praktischen Beispielen, was schnelle Erfolgerlebnisse garantiert. Außerdem bietet es als Standard-Werk auf viele Fragen, die sich bei der Umsetzung ergeben präzise und praxisnahe Antworten, ohne den Leser mit zu viel "drum herum" zu langweilen.