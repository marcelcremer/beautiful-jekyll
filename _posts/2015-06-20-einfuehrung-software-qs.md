---
layout: post
title: Einführung in das Software Qualitätsmanagement
categories: Programmierung
---
Mit diesem Artikel möchte ich den Startschuss für eine Artikelserie geben, die einen nicht unerheblichen Aspekt der Programmierung beschreibt: Das Software Testing. Deshalb befassen wir uns im folgenden zunächst einmal mit den Grundlagen von Software Fehlern und wie man Ihnen auf die Schliche kommen kann.
<!--more-->
Warum wir Software Testing benötigen
------------------------------------

> “Programming is like sex. One mistake and you have to support it for the rest of your life.” – Michael Sinz

Ich glaube die meisten  Programmierer können sich damit identifizieren. Egal wie lange man sich mit einem Thema beschäftigt hat, ob man gewissenhaft programmiert oder einfach nur eine Idee schnell zusammen gecodet hat: Fehler treten immer auf. Einige davon kann man relativ schnell identifizieren, andere kommen erst später zum Vorschein und wieder andere entstehen, weil man unter enormen Zeitdruck geänderte Anforderungen implementieren muss.  Egal wer am Ende Schuld ist - die Problemlösung bleibt am Ende beim Entwickler hängen. Doch warum entstehen eigentlich so viele Fehler und wieso ist so viel "schlechte" Software im Umlauf? Meiner Meinung nach gibt es dafür 2 Hauptgründe, die auf den ersten Blick nicht direkt sichtbar werden:

### 1\. Software-Entwicklung ist jung!

Hast du dir einmal überlegt, was man alles beachten muss um ein Gebäude zu bauen? Egal ob Kathedrale oder eine kleine Holzhütte, es spielen unglaublich viele Faktoren in den Prozess des Aufbaus mit ein. Da wäre zum Beispiel die Qualität der Steine, das Mischungsverhältnis des Mörtels, die Statik die die Last der einzelnen Komponenten bestimmen kann und so weiter und so fort. Ich bin kein Bauingeniur und habe auch sonst nicht viel Ahnung vom Häuserbau, aber mich beeindruckt die unglaubliche menschliche Leistung die nötig ist, damit eine Brücke nicht einstürzt und scheinbar mühelos LKWs tragen kann oder Unterwasserkuppeln die ohne Probleme das Wasser verdrängen und uns dadurch im Aquarium ein nahezu hautnahes erleben von Meeresbewohnern ermöglicht. Wie schafft die Menschheit das? Vor ein paar Jahrhunderten, zum Beispiel zu der schon sehr Fortschrittlichen Zeit der Römer, war es noch nicht so einfach möglich eine Brücke über den Rhein zu bauen um die "Barbaren" auf der rechtsrheinischen Seite zu bezwingen. Es gab viele Versuche und unzählige Menschen sind dabei ums Leben gekommen. Das Bauingeniurswesen ist eine Kunst, die über Jahrtausende von den Neandertalern bis heute gereift ist und bis zur Perfektion getrieben wurde. In all den Jahren wurden mitels Try & Error Prinzip Methodiken entwickelt und getestet, um diejenigen zu ermitteln, die sich als praktikabel erwiesen haben. Aus diesem Grund ist es möglich, dass wir heute ohne Probleme Brücken über den Rhein oder riesige Wolkenkratzer errichten können. Wenn wir uns mit diesem Gedanken einmal der Softwareentwicklung widmen, dann merken wir schnell, warum die Software so schlecht ist: Die Methodiken, die wir in den nicht einmal 100 Jahren Programmiergeschichte entwickelt haben sind noch mehr als in den  Kinderschuhen. Natürlich haben wir versucht, Techniken aus dem Ingenieurswesen zu übernehmen (man denke etwa an das Wasserfallmodell, die Erweiterung des Wasserfallmodells und dann das Spiralmodell, die alle nicht so effektiv sind, wie wir uns das wünschen), aber die Präzision die wir in tausenden von Jahren im Bauwesen entwickelt haben kann man in den paar Jahren Programmiererfahrung natürlich nicht erreichen. Zumal der zweite, nicht ganz so offensichtliche Punkt hier mit reinspielt:

### 2\. Software-Entwicklung ist abstrakt, komplex und schnelllebig

Ein Schreiner geht Abends nach Hause, legt die Füße hoch und berichtet seiner Frau, welchen tollen Tisch er heute zusammen gezimmert hat. Er fühlt sich toll, weil er weiß, dass er etwas geschaffen hat, das vielleicht noch in 100 Jahren Menschen dabei hilft, das Abendessen zu sich zu nehmen. Hast du das schon einmal bei der Programmierung erlebt? Nicht nur, dass der Schreiner seiner Frau die Arbeit zeigen und auf die Schönheit hinweisen kann, er kann ihr auch relativ einfach erklären, welche Schritte dafür nötig waren und worin die Eleganz seiner ganz persönlichen Arbeit liegt. Ich weiß nicht wie es euch geht, aber ich persönlich kann meiner Freundin nicht einmal erklären, was genau ich den ganzen Tag über getrieben habe - geschweige denn zeigen, was dabei herausgekommen ist oder die Eleganz meines Codes darstellen. Meine Arbeit ist rein virtuell und selbst wenn ich die Oberfläche von einem Programm präsentieren könnte, wäre diese nur die Spitze des Eisbergs. Die Softwareentwicklung beschäftigt sich grob gesagt mit abstrakter Abbildung von Bedürfnissen der echten Welt, die virtuell durch Computer befriedigt werden können. Da der Rechner die Dinge etwas anders sieht und versteht, fällt es uns schwer, die Gänze des Programms zu erfassen und die Teilprobleme die erledigt werden alle im Kopf zu haben. Dass sich dabei Fehler in der Entwicklung einstellen, sollte also kein Wunder sein. Dennoch müssen wir eine Möglichkeit finden, wie wir diese Komplexität bewältigen und überprüfen können, ob die entwickelte Software auch wirklich das tut, was wir uns vorstellen. Aus diesem  Grund hat sich das Software Testing entwickelt.

Software Testing Methoden
-------------------------

Genauso, wie Programme verschiedene Ebenen haben auf denen sich Prozesse abspielen, genauso kann man das Software Testing der einzelnen Bereiche unterscheiden. Aus diesem Grund gibt es mehrere Methoden für das Software Testing:

### Unit-Test

An unterster Stelle können wir die Unit Tests nennen. Das sind Programme, die einzelne, abgekapselte Bereiche der Software isoliert testen und somit die Funktionalität der einzelnen Softwarekomponenten sicherstellt. Im agilen Bereich des Test Driven Development hat dieser Bereich den stärksten Einfluss auf das Software Testing, da hier bereits Tests geschrieben werden, bevor die Umsetzung erfolgt.

### Integration Test

Im Software Testing sorgt der Integration Test dafür, die Einzelkomponenten miteinander "zu verheiraten" um zu testen, ob diese nicht nur einzeln sondern auch im Verbund funktionieren. Auf diese Weise werden die ersten Abhängigkeiten ausgelotet und die Funktionalität sichergestellt.

### User Acceptance Test

Bei einem User Acceptance Test (UAT) wird sichergestellt, dass die Anforderung, die der User gestellt hat auch wirklich umgesetzt wurde. Dieser Bereich des Software Testings stellt sicher, dass man nicht nur ein funktionierendes Programm hat, sondern auch der Zweck des Programms korrekt erfüllt wird. Je nach Literatur können die oberen Testszenarien in noch mehr Teiltests unterschieden werden - der Einfachheit halber möchten wir uns aber für die Grundlagen erst einmal mit den oben beschriebenen Testszenarien beschäftigen. In den folgenden Artikeln schauen wir uns daher die Testmethoden noch einmal einzeln und ausführlicher an. Außerdem überprüfen wir, welche Möglichkeiten der Testautomatisierung für Software Testing bisher entwickelt wurden und wie sinnvoll diese einsetzbar sind.