---
title: Villkorstyper för Edge-tillägg
description: Lär dig hur du definierar en biblioteksmodul av typen condition för ett edge-tillägg i Adobe Experience Platform.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Villkorstyper för kanttillägg

>[!NOTE]
>
> Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

I en taggregel utvärderas ett villkor efter att en händelse har inträffat. Alla villkor måste returnera true för att regeln ska kunna fortsätta bearbetningen. Villkorstyper tillhandahålls av tillägg och utvärderar om något är sant eller falskt, vilket returnerar ett booleskt värde.

Ett tillägg kan till exempel innehålla villkorstypen &quot;viewport contains&quot;, där användaren kan ange en CSS-väljare. När villkoret utvärderas på klientens webbplats kan tillägget hitta element som matchar CSS-väljaren och returnera om något av dem finns i användarens visningsruta.

I det här dokumentet beskrivs hur du definierar villkorstyper för ett kanttillägg i Adobe Experience Platform.

>[!IMPORTANT]
>
>Om du utvecklar ett webbtillägg läser du i handboken [villkorstyper för webbtillägg](../web/condition-types.md) i stället.
>
>I det här dokumentet förutsätts även att du känner till biblioteksmoduler och hur de är integrerade i kanttillägg. Om du behöver en introduktion kan du se översikten på [formatering av biblioteksmodul](./format.md) innan du återgår till den här guiden.

Villkorstyperna består vanligtvis av följande:

1. En vy som visas i användargränssnittet för datainsamling där användarna kan ändra inställningarna för villkoret.
2. En biblioteksmodul som skickas inom taggens körningsbibliotek för att tolka inställningarna och utvärdera ett villkor.

Om du till exempel vill utvärdera om användaren finns på värden `example.com`kan din modul se ut så här.

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
1. A [löfte](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som returnerar ett booleskt värde när det lösts.

## Kontext för modulen Bibliotek

Alla villkorsmoduler har åtkomst till en `context` variabel som anges när modulen anropas. Du kan lära dig mer [här](./context.md).
