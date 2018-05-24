---
layout: post
title: Async everything!
categories: [Programmierung, my2Cent]
comments: true
---
Am Wochenende habe ich ein Stück Servercode auf das aktuellste Release von [MassiveJS](https://github.com/dmfay/massive-js) umgestellt. Da die API ab Version 3+ komplett auf Promises aufgebaut ist und keine Option mehr bietet, sync-Befehle (die bis Massive V2 per  [deasync](https://github.com/vkurchatkin/deasync) synchronisiert wurden) auszuführen, musste ich dafür ein gutes Stück code umschreiben.<!--more-->

Mein Code beginnt nun nicht mehr "klassisch", indem ich eine Server-Klasse habe, die instanziiert und gestartet wird:

```typescript
let server = new Server();
server.start();
```

Stattdessen wird nun einfach alles "promisfiziert":

```typescript
new Promise(async (resolve) => {
    //...
    resolve(server.start();
}).catch((error) => (mainLogger || console).error(error));
```

Außerdem sind nun praktisch alle meine Methoden als async deklariert, damit ich "await" auf die Aufrufe anwenden kann. Da stellt sich einem doch schon einmal die Frage:

> WTF???

Okay, etwas sachlicher:

> Warum muss man diesen riesen Aufwand betreiben, damit per async/await Promises wie synchrone Methoden behandelt werden können, damit man vernünftig programmieren kann?

Nehmen wir mal an, wir haben einen Blogpost, zu dem der Author angegeben werden soll. Nehmen wir weiterhin an, wir haben Kommentare, zu denen wir die User ausgeben möchten.

Daraus könne man vereinfacht folgenden Promise-Code schreiben:

``` typescript
getPostAndUser = (postId) =>
{
    Promise
        .all(getBlogPost(postId), getCommentsByPostId(postId))
        .then((values) => {
            let post = values[0]; // Post-Object
            let comments = values[1]; // Comments-Array
            return Promise.all(
                Promise.resolve([post, comments], // Weitergabe der schon vorhandenen Infos
                getAuthorByPostId(postId),
                Promise.all(
                    comments
                    .map(comment => getCommentAuthorById(comment.id)) //Wir mappen die Kommentare auf "Hole den Author"-Promises und lösen diese auf
                )
            );
        })
        .then(evenMorevalues => {
            // [...] Mache irgendwas mit allen vorhandenen Informationen
        })
}
```

Okay, das ist hässlich wie die Nacht. Viel schlimmer waren Callbacks auch nicht.

Schauen wir uns das ganze nun mit Async/Await an:

``` typescript
getPostAndUser = async (postId) =>
{
    let post, comments = await getBlogPost(postId),getCommentsByPostId(postId); // paralleles holen von Post und Kommentaren
    let author, postAuthors = await getAuthorByPostId(postId), Promise.all(
                    comments
                    .map(async comment => await getCommentAuthorById(comment.id)) 
                ); // wir bekommen eine Liste von Promises zurück, also trotzdem Promise.all
    // [...] Mache irgendwas mit allen vorhandenen Informationen
}
```

Okay, das ist schon ein bisschen schicker. Trotzdem ein Heidenaufwand - vor allem weil getPostAndUser wieder ein Promise zurück gibt, das dann per "then/catch" getriggert werden muss.

Viel schöner zu Programmieren wäre es doch, wenn man den ganzen Promise-Kram nicht bräuchte, sondern einfach **ALLES** von Natur aus asynchron wäre!

Dann könnte man, ähnlich wie bei async/await, parallele Verarbeitung über mehrfachzuweisung in einer Zeile antriggern und ansonsten "synchron" programmieren, weil JS den Spaß eh im Hintergrund automatisch auflöst.

Meine Vorstellung wäre so etwas wie:

``` typescript
getPostAndUser = (postId) =>
{
    /**
      * paralleles holen von Post und Kommentaren
      * ist mir egal, wie lange das dahinter braucht - warten muss ich sowieso, bis beides da ist!!!
      */
    let post, comments = getBlogPost(postId), getCommentsByPostId(postId); 
    
    /**
      * Auch hier:
      * Warten, bis alles da ist muss ich sowieso!
      * .map-Funktionen können immer parallel ausgeführt werden
      */
    let author, postAuthors = getAuthorByPostId(postId), comments
                    .map(comment => getCommentAuthorById(comment.id))
                );       
    // [...] Mache irgendwas mit allen vorhandenen Informationen
}
```

Zu diskutieren wäre dann eigentlich nur, wie Operationen alá Array.forEach() behandelt werden.
In der Regel will man da den Funktionsaufruf wohl seriell machen, aber das könnte man ja durch Einführung eines Flags wie z.B. 

```typescript
Array.forEach(value, index, Array, serial = true)) 
```

und/oder durch eine weitere Funktion 

```typescript
Array.forEachParallel(value, index, Array)) 
```

ermöglichen.

Als Fazit glaube ich, dass Promises und Async / Await 90% der Zeit gar nicht nötig ist, aber die anderen 10% dazu führen, dass man endlos lange async / await Geflechte schreiben muss. Und dafür Sorgen muss, dass alle Funktionen als async deklariert sind. Und das der gesamte Code als Promise ausgeführt werden muss. Und ... *grummel* *grummel* *grummel*
