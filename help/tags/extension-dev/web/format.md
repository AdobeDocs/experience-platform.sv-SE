---
title: Biblioteksmoduler i webbtillägg
description: Lär dig formatera biblioteksmoduler för webbtillägg i Adobe Experience Platform.
exl-id: 08f2bb01-9071-49c5-a0ff-47d592cc34a5
source-git-commit: b3754c94843f32ba58aa1e020dface1179372de3
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Biblioteksmoduler i webbtillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

>[!IMPORTANT]
>
>Det här dokumentet innehåller biblioteksmodulformatet för webbtillägg. Om du utvecklar ett kanttillägg läser du i handboken [formatera kanttilläggsmoduler](../edge/format.md) i stället.

En biblioteksmodul är en del av återanvändbar kod som tillhandahålls av ett tillägg som släpps ut i taggens körningsbibliotek i Adobe Experience Platform. Det här biblioteket körs sedan på klientens webbplats. Till exempel en `gesture` händelsetypen kommer att ha en biblioteksmodul som körs på klientens webbplats och identifierar användargester.

Biblioteksmodulen är strukturerad som en [CommonJS, modul](https://nodejs.org/api/modules.html#modules-commonjs-modules). I en CommonJS-modul är följande variabler tillgängliga för användning:

## `require`

A `require` kan du komma åt:

1. Kärnmoduler från taggar. Dessa moduler kan nås via `require('@adobe/reactor-name-of-module')`. Se dokumentet om tillgängligt [kärnmoduler](./core.md) för mer information.
1. Andra moduler i tillägget. Alla moduler i tillägget kan nås via en relativ sökväg. Den relativa sökvägen måste börja med `./` eller `../`.

Exempelanvändning:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## `module`

En kostnadsfri variabel med namnet `module` är tillgängligt så att du kan exportera modulens API.

Exempelanvändning:

```javascript
module.exports = function(…) { … }
```

## `exports` {#exports-variable}

En kostnadsfri variabel med namnet `exports` är tillgängligt så att du kan exportera modulens API.

Exempelanvändning:

```javascript
exports.sayHello = function(…) { … }
```

Detta är ett alternativ till `module.exports` men användningen är mer begränsad. Läs [Modulen.export och export i node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) för en bättre förståelse av skillnaderna mellan `module.exports` och `exports` och tillhörande kavattar med `exports`. Gör livet enklare och använd `module.exports` i stället för `exports`.

## Körning och cachning

När taggens körningsbibliotek körs &quot;installeras&quot; modulerna omedelbart och deras export cachelagras. Anta följande modul:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` loggas omedelbart medan `runs when necessary` loggas endast när den exporterade funktionen anropas av taggmotorn. Det kan vara onödigt för just din modul, men du kan utnyttja detta genom att göra de inställningar som behövs innan du exporterar funktionen.
