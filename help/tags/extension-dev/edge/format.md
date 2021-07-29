---
title: Biblioteksmoduler i Edge-tillägg
description: Formatera biblioteksmoduler för taggtillägg i en edge-egenskap.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Biblioteksmoduler i edge-tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

>[!IMPORTANT]
>
>Det här dokumentet beskriver biblioteksmodulens format för kanttillägg. Om du utvecklar ett webbtillägg läser du i guiden [formatera webbtilläggsmoduler](../web/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i kodkörningsbiblioteket i Adobe Experience Platform (biblioteket som körs på edge-noden). En `sendBeacon`-åtgärdstyp kommer till exempel att ha en biblioteksmodul som körs på kantnoden och skickar en fyr.

Biblioteksmodulen är strukturerad som en [CommonJS-modul](http://wiki.commonjs.org/wiki/Modules/1.1.1). I en CommonJS-modul är följande variabler tillgängliga för användning:

## [!DNL require]

Du kan använda en `require`-funktion för att komma åt moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempelanvändning:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

Det finns en kostnadsfri variabel med namnet `module` som gör att du kan exportera modulens API.

Exempelanvändning:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

Det finns en kostnadsfri variabel med namnet `exports` som gör att du kan exportera modulens API.

Exempelanvändning:

```js
exports.sayHello = (…) => { … }
```

Detta är ett alternativ till `module.exports`, men användningen är mer begränsad. Läs [Understanding module.exporting and exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för att få en bättre förståelse för skillnaderna mellan `module.exports` och `exports` och de relaterade grottorna med `exports`. Gör livet enklare när du är osäker och använd `module.exports` istället för `exports`.

## Modulsignatur på serversidan

Alla modultyper (dataelement, villkor eller åtgärder) som tillhandahålls av tillägget anropas med samma parametrar: [kontext](./context.md).

```js
exports.sayHello = (context) => { … }
```
