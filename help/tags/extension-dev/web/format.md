---
title: Biblioteksmoduler i webbtillägg
description: Lär dig formatera biblioteksmoduler för webbtillägg i Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: b3754c94843f32ba58aa1e020dface1179372de3
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Biblioteksmoduler i webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

>[!IMPORTANT]
>
>Det här dokumentet innehåller biblioteksmodulformatet för webbtillägg. Om du utvecklar ett kanttillägg läser du i handboken om [att formatera kanttilläggsmoduler](../edge/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i taggens körningsbibliotek i Adobe Experience Platform. Det här biblioteket körs sedan på klientens webbplats. En `gesture`-händelsetyp har till exempel en biblioteksmodul som körs på klientens webbplats och identifierar användargester.

Biblioteksmodulen är strukturerad som en [CommonJS-modul](https://nodejs.org/api/modules.html#modules-commonjs-modules). I en CommonJS-modul är följande variabler tillgängliga för användning:

## `require`

Du har tillgång till en `require`-funktion:

1. Kärnmoduler från taggar. Dessa moduler kan nås via `require('@adobe/reactor-name-of-module')`. Mer information finns i dokumentet om tillgängliga [kärnmoduler](./core.md).
1. Andra moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempel:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

Det finns en kostnadsfri variabel med namnet `module` som gör att du kan exportera modulens API.

Exempel:

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

Det finns en kostnadsfri variabel med namnet `exports` som gör att du kan exportera modulens API.

Exempel:

```javascript
exports.sayHello = function(…) { … }
```

Det här är ett alternativ till `module.exports`, men användningen är mer begränsad. Läs [Om module.exporting och exporting in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för att få en bättre förståelse för skillnaderna mellan `module.exports` och `exports` och de relaterade grottorna med `exports`. Gör livet enklare när du är osäker och använd `module.exports` i stället för `exports`.

## Körning och cachning

När taggens körningsbibliotek körs &quot;installeras&quot; modulerna omedelbart och deras export cachelagras. Anta följande modul:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` loggas omedelbart medan `runs when necessary` endast loggas när den exporterade funktionen anropas av taggmotorn. Det kan vara onödigt för just din modul, men du kan dra nytta av detta genom att göra de inställningar som behövs innan du exporterar funktionen.
