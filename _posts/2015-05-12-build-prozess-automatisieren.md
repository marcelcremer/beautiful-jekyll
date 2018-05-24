---
layout: post
title: Den Build Prozess automatisieren
categories: Programmierung
---

Anders als bei gewöhnlichen „Produkten“, die in der Wirtschaft hergestellt werden, kann man die Qualität von Software in der Regel schlecht messen. <!--more-->Aufgrund dessen gibt es viele Unternehmen, die entweder schlechte Programme, oder schwankende Qualität an Ihre Kunden abliefern. Wie also kann man sicherstellen, dass das, was der Kunde für sein Geld bekommt immer gleichbleibende Qualität aufweist? Zunächst einmal sollte man sich die Software, die produziert wird anschauen und herausarbeiten, welche Art von Software man bereitstellt. Wenn man ein „Produkt“ herstellt, also eine Software die losgelöst von anderen Programmen Ihre Funktion ausführt, kann man den Qualitätsstandard zumindest auf die Auslieferung festlegen: Das gelieferte Produkt sollte immer gleich aufgebaut sein, sich gleich installieren lassen und mit geringem Testaufwand zum Einsatz gebracht werden können (Dies gilt im Übrigen auch für Plugins, die immer eine gleiche Struktur aufweisen). In diesen Fällen gillt, dass man ohne Probleme den Build Prozess automatisieren kann. Anders verhält es sich hingegen mit Anpassungen vorhandener Software-Produkte: Nach Abschluss der Entwicklungsphase werden viele verschiedene Anpassungen, entweder in Form von „Teilskripten“ oder von mehreren Ausführungsschritten erstellt, die vielleicht in verschiedene Teilbereiche der Grundsoftware eingreift. Aber auch hier können gewisse Dinge automatisiert werden, sodass der Kunde es leichter hat, die betreffende Software bei sich einzusetzen.

**Wie kann man einen Build Prozess automatisieren?**
----------------------------------------------------

 

1.  An erster und wichtigster Stelle für alle Softwareprojekte steht die **Versionierung von Teil-, Test- und Produktivständen**. Es gibt nichts schlimmeres für ein Entwicklungsteam, als unversionierte Software, bei der der Kunde in der Produktionsumgebung ein Problem hat, in der Testumgebung schon ein neuere Stand zu testen ist, in der Entwicklung gerade an einem anderen Feature gearbeitet wird und niemand die Möglichkeit hat, zwischen den verschiedenen Versionsständen hin- und herzuwechseln.

  Verschiedene Versionskontrollsysteme wie CVS, SVN, Mercurial, Git und andere erfüllen die obigen Anforderungen mehr oder weniger gut. Welches Versionskontrollsystem zu wem passt, sollte jeder für sich selbst herausfinden. Ich empfehle eigentlich immer Git, denn es ist schlank, leicht zu lernen und eines der mächtigsten Systeme die angeboten werden (und dazu kostenlos ;-) )

1.  Wenn die Software ausgeliefert wird, werden **bestimmte Schritte immer und immer wieder wiederholt**. Diese Schritte gilt es zu identifizieren und zu automatisieren. Beispiele dafür sind:
    1.  Umkopieren von Ordnern
    2.  Versionsnummer eintragen
    3.  Nicht benötigte Dateien (Versionskontrolldateien, Logdateien, Testdateien,…) entfernen
    4.  Den Ordner zippen oder ein Setup daraus bauen
    5.  Das fertige Produkt hochladen
    6.  …

Das Tool, das ich dazu benutze ist Ant oder NAnt im .Net-Umfeld. Ant ist leicht zu erlernen und schnell implementiert. Andere Tools wie beispielsweise Maven leisten zwar deutlich komplexere Arbeit (z.B. die Bereitstellung von immer gleichem Projektarbeitsbereichen, das Regeln von Abhängigkeiten etc.), die Einarbeitungszeit steht aber meiner Meinung nach in keinem Verhältnis zum späteren Nutzen.

1.  Optional: Im letzten Abschnitt bin ich bereits auf die Auflösung von Abhängigkeiten eingegangen. Bei größeren Projekten hat man oftmals mehrere, **voneinander abhängige Module** die für den Build-Prozess herangezogen werden müssen. Damit diese Module nicht mehrmals vorgehalten werden müssen und die richtigen Versionsabhängigkeiten auflösen, empfiehlt es sich, entweder Systeme wie Maven zu benutzen, die solche Abhängigkeiten von Haus aus auflösen können, oder eigenständige Systeme wie z.B. Ivy einzuführen, die genau dasselbe tun. Welches System für einen am besten geeignet ist, muss jeder für sich selber herausfinden.
2.  **Continous Integration Systeme** benutzen. Was bedeutet das? Nun, da jeder Build-Prozess automatisiert ist, sollte sich jede Version die wir bauen immer gleich Verhalten und den gleichen Output produzieren – theoretisch. In der Praxis ist es aber leider so, dass aber gerade bei wachsenden Software Projekten über mehrere Entwicklungszyklen hinweg die Rahmenbedingungen oft verändert werden. Da werden abhängige Module entfernt, weil niemand mehr weiß, ob sie benutzt werden oder Software aktualisiert, wobei die neue Version nicht mehr mit dem alten Build Prozess kompatibel ist usw.. Aus diesem Grund gibt es sogenannte **Continous Integration Systeme**, die den Build-Prozess für einen ausführen und die dabei erzeugten „Artefakte“, also fertigen Module oder Plugins archivieren. So ist es auch nach Jahren noch möglich, die entsprechenden Versionen abzurufen und zu sehen, was der Kunde wirklich bekommen hat und nicht nur, was er vielleicht bekommen hat. Die bekanntesten Vertreter der Continous Integration Systeme sind Jenkins im Open Source Bereich und Bamboo als kostenpflichtiges Tool, dass sich nahtlos in die Atlassian-Produktreihe integrieren lässt.

Wenn man die oben genannten Punkte befolgt, kann man einen nahtlosen Build-Prozess implementieren, der nicht mehr als einen Klick im Continous Integration System benötigt, um ein immer gleiches Software Produkt zu erzeugen. Das spart zum einen Zeit, zum anderen verhindert es aber auch, dass sich menschliche Fehler (z.B. vergessen, die nicht benötigten Dateien zu entfernen oder die Versionsnummer hochzusetzen) einschleichen und der Kunde bekommt ein immer gleich bleibendes Produkt, das besser gewartet und auch in älteren Software-Ständen benutzt werden kann.