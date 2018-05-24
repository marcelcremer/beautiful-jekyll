---
layout: post
title: AngularJS - Trendframework unter die Lupe genommen
categories: Programmierung
---
Immer wieder tauchen neue Frameworks auf, die die Entwickler-Welt begeistern. Als Smart Programmer sollte man mit dem Trend der Zeit gehen und neue Technologien zumindest beurteilen können. Aus diesem Grund gibt es diese Woche einen Bericht über das JavaScript Trendframework AngularJS.
<!--more-->
2-Way Databinding mit AngularJS
-------------------------------

Wer sich ein bisschen mit AngularJS beschäftigt, wird zunächst einmal auf den Begriff "2 Way Databinding" stoßen, der laut vielen Seiten als Hauptvorteil von AngularJS beschrieben wird. 2-Way Databinding bedeutet, dass Informationen von der Präsentationsschicht (bei AngularJS das HTML-Form) direkt in den Controller und zurück befördert werden. Das bedeutet, ich kann einzelnen Formularelementen direkt ein Model zuweisen und dieses wird synchron gehalten - selbst wenn ich mehrere Formularelemente mit dem gleichen Model verknüpfe. Das funktioniert mit AngularJS über die sogenannte ng-model Direktive: Man beschreibt ein HTML-Element mit dem zusätzlichen Element ng-model="_<JavaScript-Variable>_" und AngularJS mappt den Inhalt des Elementes automatisch mit der entsprechenden JavaScript-Variablen in einem bestimmten Scope. Das geschieht unter Benutzung von jQuery durch einenen nachgelagerten Parser, der die Attribute nach vollständigem Laden des DOMs entsprechend anbindet.

Über Scopes in AngularJS
------------------------

Damit in AngularJS variablen etc. gemapped und mehrfach verwendet werden können, gibt es hier Scopes die über bestimmte Controller definiert werden. Über die Direktive ng-controller="" wird ein bestimmter Bereich als "zu diesem Controller zugehörig" markiert. Auf diese Weise hat man direkten Einfluss auf die Bereiche in einem oder mehreren HTML-Files, die von einem bestimmten Controller verwaltet werden. Der Scope wird dabei, genau wie Services, Factories etc. in einen bestimmten Controller injiziert. Durch die damit erzeugte Dependency Injection wird AngularJS leicht testbar, da es somit einfacher ist, Daten und Services vorzutäuschen (Mocken).

Mit ng-repeat über AngularJS Tabellen befüllen
----------------------------------------------

Ein weiteres wichtiges Feature aus meiner Sicht ist die Möglichkeit, über ng-repeat Arrays und deren Inhalte automatisch via HTML auszugeben. So hat man beispielsweise die Möglichkeit, sich Arrays von Objekten via RESTful Services zu holen und diese direkt ins HTML auzugeben. Selbst verschachtelte Elemente sind kein Problem, so dass serverseitige Programmierung an dieser Stelle obsolet wird.

10 weitere Features, über die nur unzureichend berichtet wird
-------------------------------------------------------------

### 1\. Services und Factories

Über Services und Factories kann man mit AngularJS selbst definierte Datenquellen erstellen und diese beliebig austauschen. Ein Service kann dabei z.B. sein, dass man Daten via Ajax holt. Bei einem Mock-Service könnte man diesen z.B. mit einem vordefinierten JSON befüllen, damit angenommen wird, dass die Daten immer korrekt zurückkommen.

### 2\. Animation mit AngularJS

Über AngualarJS kann man verschiedene Formen von Animationen erzeugen. So ist es zum Beispiel möglich, zwischen verschiedenen CSS Klassen zu tweenen oder ander vorab festgelegte Aktionen auszuführen, um die eigene Applikation lebhafter erscheinen zu lassen.

### 3\. Eigene Direktiven

Mit AngularJS kann man eigene Direktiven erstellen. Das bedeutet, dass man ein bestimmtes HTML-Tag mit der entsprechenden Direktive ausstatten kann und dahinter eigene Funktionen hinterlegen oder Datenmanipulationen ausführen kann.

### 4\. Klassenmanipulation

Über AngularJS kann man die Klassen von HTML-Tags ohne Probleme austauschen, verstecken oder auf bestimmte Bedingungen hin setzen. Auf diese Weise kann man über den Controller bequem steuern, wie die Ausgangsseite am Ende aussehen soll und zur Laufzeit Änderungen vornehmen.

### 5\. Filtermöglichkeiten

Ein wichtiges Feature, vor allem aber nicht nur für den Bereich ng-repeat ist es, dass AngularJS Filter benutzen kann um per JavaScript z.B. Objekt-Arrays zu filtern. Auf diese Weise sind Suchfunktionen kein Problem mehr!

### 6\. Routing für SPAs (Single Page Applications)

Über die Möglichkeit, die URLs zu parsen und entprechend andere Views einzublenden kann man mit AngularJS im handumdrehen SPAs (Single Page Applications) erzeugen. Das sorgt für eine klare Struktur und einheitlichen Code.

### 7\. TouchScreen Unterstützung

AngularJS bietet von Haus aus die Möglichkeit, die Webseite z.B. durch die Benutzung von Swipes (über den Bildschirm wischen) verschiedene Aktionen auszuführen. Auf diese Weise ist es möglich, die Webseite von Beginn an auf mobile Endgeräte zu optimieren.

### 8\. Eigene Checkbox-Werte und Validierung

Durch verschiedene Direktiven, die direkt in das entsprechende Input-Tag eingefügt werden kann man mit AngularJS unter anderem festlegen, welche Werte das Model annehmen sollen, wenn das entsprechende Input-Feld befüllt wird. So kann man zum Beispiel einen Wert auf "42" setzen wenn eine bestimmte Checkbox aktiviert wird, ohne dass man dies umständlich programmieren müsste. Außerdem kann man mit AngularJS Formularvalidierungen ermöglichen (Textbox muss Email-Adresse enthalten, Name muss n Zeichen haben,...), so dass der User sofortiges Feedback zu seinen Aktionen bekommt, noch bevor die Daten an den Server übermittelt werden.

### 9\. Cache-Control

Über AngularJS ist es ohne weiteres möglich, das Caching der Webseiten zu beeinflussen und dadurch wertvolle Zeit beim Rendering der HTML-Seiten zu sparen.

### 10\. Helper-Funktionen

Neben den ganzen Funktionalitäten die bereits erläutert werden, stellt AngularJS auch alle Funktionen die sie selbst benutzen um bestimmte Aktionen auszuführen, selbige als Helper-Funktionen bereit. So ist es ohne Probleme möglich, beispielsweise die Filter-Funktion der Direktiven auch auf Model-Ebene aufzurufen oder Arrays zu sortieren, ohne dafür weitere Bibliotheken zu benutzen.

Nachteile von AngularJS
-----------------------

Jedes noch so mächtige Framework hat auch Nachteile, die ich an dieser Stelle natürlich nicht verschweigen möchte. Im Falle von AngularJS ist dies zum Beispiel die Fehlersuche: Da das komplette DOM mehrfach zur Laufzeit geparsed wird, sind die Fehlermeldungen die AngularJS wirft mehr als kryptisch. Teilweise bekommt man auch gar keine Fehlermeldung - es passiert einfach nichts. Da AngularJS komplett client-seitig ausgeführt wird, sollte man Benutzereingaben die bereits vorvalidiert wurden aus Sicherheitsaspekten immer auf dem Server noch einmal nachvalidieren, sonst macht man seine Applikation sehr schnell angreifbar. Ausserdem sind die ganzen Direktiven die AngularJS bereitstellt von der Syntax her relativ gewöhnungsbedürftig, sodass es bei mir zum Beispiel häufiger vorkommt, dass ich noch einmal nachschauen oder mit "Try and Error" probieren muss, bis mir eine Funktionalität so gelingt, wie ich mir das vorstelle. Ein weiterer Nachteil, den man aber leicht in den Griff bekommt, ist die HTML-validierung: Um AngularJS zu benutzen, muss man HTML-Elementen neue Properties (Direktiven) hinzufügen, die im W3C-Schema nicht vorgesehen ist. Aus diesem Grund sollte man immer die Schreibweise data-ng-_<Direktivenname>_ anstatt ng-_<Direktivenname>_ verwenden_\-_ dies gewährleistet, dass der W3C-Validator die neuen Properties als Custom Properties erkennt und damit als valide einstuft.

Fazit und weitere Quellen
-------------------------

AngularJS ist meiner Meinung nach ein großartiges Framework für die Webentwicklung. Dennoch muss man sich einige Zeit mit diesem Framework und der Vorgehensweise beschäftigen, um brauchbare Ergebnisse zu bekommen. Das suboptimale Fehlerhandling und die z.T. etwas gewöhnungsbedürftige Syntax erlauben es mir leider nur, 4 von 5 Sternen zu vergeben. Das Framework mit weiterer Dokumentation findet ihr [hier](https://angularjs.org/). Außerdem kann ich euch eine wunderbare Schnelleinführung von dem Microsoft-Entwickler Dan Wahlin empfehlen: [AngularJS in 60ish Minutes](https://youtu.be/i9MHigUZKEM).