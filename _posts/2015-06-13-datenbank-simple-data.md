---
layout: post
title: Datenbankprogrammierung mit Simple.Data
categories: Programmierung
---
In meinem [ersten Artikel zum Thema ORM](../einfuehrung-orm/) habe ich bereits eine kurze Einführung in das Thema ORM gegeben. Mit diesem Artikel möchte ich eine weitere Möglichkeit vorstellen, wie man die Datenbankprogrammierung im .Net-Umfeld abstrahieren kann.
<!--more-->
### Simple.Data

Das Framework Simple.Data wird auf der [Homepage](http://simplefx.org/simpledata/docs/index.html) beschrieben als "\[...\] a lightweight framework that uses the dynamic features of .NET 4 to provide an expressive, ORM-ish way of accessing and manipulating data without any of the code pre-generation and boilerplate required by other frameworks". Wow, den Satz müssen wir erst einmal verdauen: Simple.Data ist also

*   ein leichtgewichtiges Framework
*   benutzt "[dynamic Objects](http://www.smart-programmer.de/smart-lexikon/dynamic-net/)" um die Datenbankobjekte zu binden
*   fühlt sich "ORM"-mäßig an
*   benötigt kein Mapping und keine vordefinierten Objekte wie andere ORM-Frameworks

Das klingt doch schon einmal vielversprechend, ist doch das Mapping und die Erstellung von Plain Old Objects ein entscheidender Nachteil von ORM-Frameworks.

### Wie bindet man Simple.Data ein?

Um Simple.Data in seinem Projekt zu benutzen, stehen praktische Nuget-Pakete zur Verfügung. Aus diesem Grund reicht es, sich einfach das Paket von Simple.Data in dem entsprechenden Datenbankdialekt herunterzuladen. Als Abhängigkeit wird dann noch Simple.Data.Core heruntergeladen und schon kann man Simple.Data in seinem Projekt benutzen.

### Die erste Datenbankverbindung

Um eine Verbindung zur Datenbank aufzubauen hat man mehrere Möglichkeiten. Die einfachste ist, wenn man den DefaultConnectionString in der App.Config setzt. Dann kann man mit einem einfachen

var db = Database.Open();

ein neues Simple.Data Datanbankobjekt erzeugen. Falls man mehrere ConnectionStrings angegeben hat, kann man mit

var db = Database.OpenNamedConnection("myConnectionStr1");

den entsprechenden ConnectionString aufrufen.  Die letzte Methode ist, den Connectionstring und optional auch den Provider sofort explizit anzugeben:

var db = Database.OpenConnection("myconStr1", "providerString");

Damit haben wir bereits eine Verbindung zur Datenbank - die Definition "leichtgewichtig" ist dafür schon fast zu schwach.

### Ein erster Query mit Simple.Data

Nun wollen wir natürlich auch Daten haben und das unabhängig davon, ob ich nun eine NoSQL-Datenbank oder eine SQL-Datenbank habe. Auch das lässt sich mit Simple.Data "simple" erledigen:

var person = db.Persons.FindByName("Marcel Cremer");

Auch hier kann man vertrauensvoll von "leichtgewichtig" sprechen. Damit wir auch verstehen, was passiert, möchte ich das ganze kurz aufschlüsseln:

1.  Unser Simple.Data Objekt ist ein dynamic Objekt, deshalb können wir auf den Tabellennamen einfach via Property zugreifen
2.  FindBy ist eine Methode, die via Reflection aufgelöst wird. Aus diesem Grund können wir FindByName schreiben und Simple.Data weiß, was zu tun ist
3.  Wir bekommen ein IEnumerable zurück, dass dynamische Objecte vom Typ Simple.Record enthält. Über diese können wir iterieren und bekommen so alle Treffer, die Simple.Data gefunden hat

### LINQ-Unterstützung

Nicht nur der Zugriff, sondern auch die Arbeit mit den entsprechenden Simple.Data Objekten ist einfach. So kann man z.B. einfach mit einem LINQ-Like-Methodenaufruf die erste Person der Ergebissmenge holen:

var person = db.Persons.FindByName("Marcel Cremer").FirstOrDefault();
Console.WriteLine(Person.Name ?? "Nothing found");
//Writes: "Marcel Cremer" or "Nothing found"

### Daten modifizieren mit Simple.Data

Das man auch Daten mit Simple.Data schnell modifizieren kann, sieht man im folgenden:

db.Persons.UpdateAll(Name: "Homer Simpson", Age: 50, Condition: Name == "Marcel Cremer");

Auch hier macht sich Simple.Data Reflections zunutze und erstellt unter SQL-Datenbanken einen Query, der in etwa so aussieht:

Update Persons SET Name="Homer Simpson",Age=50 WHERE Name="Marcel Cremer"

Unsere Condition wird also in Standard .Net-Notation angegeben und entsprechend in die Where-Clause eingefügt.

### Fazit

Simple.Data ist ein wahnsinnig gutes, ORM ähnliches Framework das das prädikat "leichtgewichtig" mehr als verdient hat. Außer dem Connection String sowie dem einbinden der Pakete für Framework und Datenbankdialekte gibt es nichts zu tun! Die Objekte werden per Reflection erzeugt und aufgelöst und die generierten Queries sind sehr sauber. Ich kann jedem  der mit .Net arbeitet nur empfehlen, dieses Framework einmal auszuprobieren. Ich habe in nunmehr 3 Monaten Arbeit mit diesem Framework nur ein Manko festgestellt: Es ist  nicht immer einfach zu erkennen, wann man mit eckigen Klammern \[\] auf die Properties zugreifen kann und wann nicht. Aus diesem Grund gestaltet es sich teilweise etwas schwierig, auf Tabellen und Properties zuzugreifen, die erst zur Laufzeit bekannt sind. Auch die Syntax ist etwas gewöhnungsbedürftig, weshalb man manchmal ein bisschen herumprobieren muss, bis das man auf das Ergebnis kommt, dass man gerne haben möchte. Aus diesem Grund habe ich dem Framework nur 4 von 5 Sternen gegeben.