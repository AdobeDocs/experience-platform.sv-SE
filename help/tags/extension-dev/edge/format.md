---
title: Biblioteksmoduler i Edge-tillägg
description: Formatera biblioteksmoduler för taggtillägg i en edge-egenskap.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Biblioteksmoduler i edge-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

>[!IMPORTANT]
>
>Det här dokumentet beskriver biblioteksmodulens format för kanttillägg. Om du utvecklar ett webbtillägg läser du i handboken om [att formatera webbtilläggsmoduler](../web/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i kodkörningsbiblioteket i Adobe Experience Platform (biblioteket som körs på edge-noden). En `sendBeacon`-åtgärdstyp kommer till exempel att ha en biblioteksmodul som körs på kantnoden och skickar en fyr.

Biblioteksmodulen är strukturerad som en [CommonJS-modul](https://nodejs.org/api/modules.html#modules-commonjs-modules). I en CommonJS-modul är följande variabler tillgängliga för användning:

## [!DNL require]

Du har tillgång till en `require`-funktion för att komma åt moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempel:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Det finns en kostnadsfri variabel med namnet `module` som gör att du kan exportera modulens API.

Exempel:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Det finns en kostnadsfri variabel med namnet `exports` som gör att du kan exportera modulens API.

Exempel:

```js
exports.sayHello = (…) => { … }
```

Det här är ett alternativ till `module.exports`, men användningen är mer begränsad. Läs [Om module.exporting och exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för att få en bättre förståelse för skillnaderna mellan `module.exports` och `exports` och de relaterade grottorna med `exports`. Gör livet enklare när du är osäker och använd `module.exports` i stället för `exports`.

## Modulsignatur på serversidan

Alla modultyper (dataelement, villkor eller åtgärder) som tillhandahålls av tillägget anropas med samma parametrar: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
