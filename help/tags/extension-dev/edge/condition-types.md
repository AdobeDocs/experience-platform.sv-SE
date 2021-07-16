---
title: Villkorstyper för Edge-tillägg
description: Lär dig hur du definierar en biblioteksmodul av typen condition för ett edge-tillägg i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Villkorstyper för kanttillägg

>[!NOTE]
>
> Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

En biblioteksmodul av typen condition utvärderar om något är sant eller falskt och returnerar ett booleskt värde.

>[!IMPORTANT]
>
>Det här dokumentet innehåller villkorstyper för kanttillägg. Om du utvecklar ett webbtillägg läser du i guiden om [villkorstyper för webbtillägg](../web/condition-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i taggtillägg. Om du behöver en introduktion läser du översikten om [biblioteksmodulens formatering](./format.md) innan du går tillbaka till den här guiden.

Om du till exempel vill utvärdera om användaren finns på värden `example.com` kan din modul se ut så här.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Om du vill göra värdnamnet konfigurerbart av användaren för att tillåta indata för ett värdnamn och spara det i inställningsobjektet, kan objektet se ut ungefär som i det här exemplet.

```js
{
  "hostname": "example.com"
}
```

Om du vill använda det användardefinierade värdnamnet måste modulen ändras till följande:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Villkorsresultat

Resultatet som returneras av en villkorsmodul kan vara något av följande:

1. Ett booleskt värde (`true` eller `false`).
1. Ett [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som returnerar ett booleskt värde när det lösts.

## Kontext för modulen Bibliotek

Alla villkorsmoduler har åtkomst till en `context`-variabel som anges när modulen anropas. Du kan läsa mer [här](./context.md).
