---
layout: post
title: Angular 2 - Relative Pfade zu Templates
categories: Programmierung
---

*Achtung: Dieser Artikel gehört zu den "alten" Versionen von ng2. Mit Webpack sind diese Probleme nicht mehr vorhanden!*

Warum zum Teufel findet Angular 2 meine Template-Dateien nicht, wenn ich relative Pfadangaben benutze? Genau das habe ich mich auch gefragt. Hier die Antwort...<!--more-->  Sagen wir, wir haben einen Dateibaum der in etwa so aussieht:  
|-app  
|--app.component.ts   
|--app.component.css   
|--app.component.html   
Und nehmen wir an, wir haben ein Beispielmodul à la:

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'selector',
    templateUrl: 'app.component.html',
    styles: \['app.component.css'\]
})
export class ExampleAppComponent implements OnInit {
    constructor() { }

    ngOnInit() { }
}

Dann werdet ihr bestimmt das gleiche Problem haben wie ich. Angular2 meckert darüber, dass es die Templates nicht finden kann und sucht im falschen Pfad. Woran liegt das? Nun, der Systemloader geht standardmäßig davon aus, dass alle Komponenten die nicht in dem gleichen Modul wie die Applikation sind absolute Pfade zu ihren Templates angeben. Aus diesem Grund sucht der Systemloader standardmäßig auch immer absolut in eurem Projekt, es sei denn, ihr gebt explizit an, dass eure Komponente zum Applikationsmodul gehört. Die Vorgehensweise ist dafür für Commonjs und Systemjs unterschiedlich. Wer Visual Studio Code mit den TypeScript-Templates von John Papa verwendet, dem wird aufgefallen sein, dass das Template folgenden Code erzeugt:

import { Component, OnInit } from '@angular/core';

@Component({
    moduleId: module.id,
    selector: 'selector',
    templateUrl: 'name.component.html'
})
export class ComponentNameComponent implements OnInit {
    constructor() { }

    ngOnInit() { }

}

Der erzeugte Code ist für CommonJS als Applikationsloader vorgesehen und funktioniert damit auch prächtig. Wer dagegen wie ich SystemJS benutzt, muss statt `moduleId: module.id,` die von SystemJS bereitgestellte Konstante `__moduleName` verwenden. Visual Studio Code erkennt diese aber nicht und erzeugt eine Warnung, das \_\_moduleName nicht bekannt sei. Aus diesem Grund deklarieren wir \_\_moduleName einfach in der Komponente und kommen so auf den folgenden Code, der anstandslos und Fehlerfrei akzeptiert wird:

import { Component, OnInit } from '@angular/core';
declare var __moduleName : string;
@Component({
    moduleId: __moduleName,
    selector: 'selector',
    templateUrl: 'name.component.html'
})
export class ComponentNameComponent implements OnInit {
    constructor() { }

    ngOnInit() { }

}

et voilà: Schon können wir ohne Probleme relative Pfade in Angular 2 benutzen :)