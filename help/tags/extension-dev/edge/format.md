---
title: Biblioteksmoduler i Edge-tillägg
description: Formatera biblioteksmoduler för taggtillägg i en edge-egenskap.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Biblioteksmoduler i edge-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

>[!IMPORTANT]
>
>Det här dokumentet beskriver biblioteksmodulens format för kanttillägg. Om du utvecklar ett webbtillägg läser du i handboken [formatera webbtilläggsmoduler](../web/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i kodkörningsbiblioteket i Adobe Experience Platform (biblioteket som körs på edge-noden). Till exempel en `sendBeacon` åtgärdstypen har en biblioteksmodul som körs på kantnoden och skickar en fyr.

Biblioteksmodulen är strukturerad som en [CommonJS, modul](https://nodejs.org/api/modules.html#modules-commonjs-modules). I en CommonJS-modul är följande variabler tillgängliga för användning:

## [!DNL require]

A `require` -funktionen är tillgänglig så att du kan komma åt moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempelanvändning:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

En kostnadsfri variabel med namnet `module` är tillgängligt så att du kan exportera modulens API.

Exempelanvändning:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

En kostnadsfri variabel med namnet `exports` är tillgängligt så att du kan exportera modulens API.

Exempelanvändning:

```js
exports.sayHello = (…) => { … }
```

Detta är ett alternativ till `module.exports` men användningen är mer begränsad. Läs [Modulen.export och export i node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för en bättre förståelse av skillnaderna mellan `module.exports` och `exports` och tillhörande kavattar med `exports`. Gör livet enklare och använd `module.exports` i stället för `exports`.

## Modulsignatur på serversidan

Alla modultyper (dataelement, villkor eller åtgärder) som tillhandahålls av tillägget anropas med samma parametrar: [kontext](./context.md).

```js
exports.sayHello = (context) => { … }
```
