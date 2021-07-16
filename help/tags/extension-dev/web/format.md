---
title: Biblioteksmoduler i webbtillägg
description: Lär dig formatera biblioteksmoduler för webbtillägg i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Biblioteksmoduler i webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

>[!IMPORTANT]
>
>Det här dokumentet innehåller biblioteksmodulformatet för webbtillägg. Om du utvecklar ett kanttillägg läser du i guiden [formatera kanttilläggsmoduler](../edge/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i taggens körningsbibliotek i Adobe Experience Platform. Det här biblioteket körs sedan på klientens webbplats. En `gesture`-händelsetyp har till exempel en biblioteksmodul som körs på klientens webbplats och identifierar användargester.

Biblioteksmodulen är strukturerad som en [CommonJS-modul](http://wiki.commonjs.org/wiki/Modules/1.1.1). I en CommonJS-modul är följande variabler tillgängliga för användning:

## [!DNL require]

Du har tillgång till en `require`-funktion:

1. Kärnmoduler från taggar. Dessa moduler kan nås via `require('@adobe/reactor-name-of-module')`. Mer information finns i dokumentet om tillgängliga [kärnmoduler](./core.md).
1. Andra moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempelanvändning:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

Det finns en kostnadsfri variabel med namnet `module` som gör att du kan exportera modulens API.

Exempelanvändning:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

Det finns en kostnadsfri variabel med namnet `exports` som gör att du kan exportera modulens API.

Exempelanvändning:

```javascript
exports.sayHello = function(…) { … }
```

Detta är ett alternativ till `module.exports`, men användningen är mer begränsad. Läs [Understanding module.exporting and exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för att få en bättre förståelse för skillnaderna mellan `module.exports` och `exports` och de relaterade grottorna med `exports`. Gör livet enklare när du är osäker och använd `module.exports` istället för `exports`.

## Körning och cachning

När taggens körningsbibliotek körs &quot;installeras&quot; modulerna omedelbart och deras export cachelagras. Anta följande modul:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` loggas omedelbart, medan loggas endast när den exporterade funktionen anropas av taggmotorn.  `runs when necessary` Det kan vara onödigt för just din modul, men du kan utnyttja detta genom att göra de inställningar som behövs innan du exporterar funktionen.
