---
title: applyPropositions
description: Återge utkast som redan har återgetts med sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# `applyPropositions`

Med kommandot `applyPropositions` kan du återge utkast som redan har återgetts med kommandot [`sendEvent`](sendevent/overview.md). Det här kommandot är användbart när du arbetar med enkelsidiga program där delar av sidan återges på nytt och eventuellt skriver över befintliga anpassningar av sidan.

Det här kommandot stöder följande fält:

* **Föreslag**: En array med objekt som du vill återge på nytt.
* **Visningsnamn**: Namnet på den vy som ska återges. Visningsmeddelandena för dessa beslut cachelagras och kan inkluderas i ett efterföljande `sendEvent`-kommando med alternativet `personalization.includeRenderedPropositions`.
* **Meta-data**: Ett objekt som avgör hur HTML kan användas. Den innehåller följande egenskaper:
   * Omfång
   * Väljare
   * Åtgärdstyp

Kör kommandot `applyPropositions` när du anropar den konfigurerade instansen av Web SDK. Objektet som innehåller konfigurationsalternativ har stöd för följande fält:

* **`propositions`**: En array med objekt som du vill återge igen. Det här objektet används vanligtvis inte, eftersom fältet `propositionScopes` vanligtvis avgör vilka omfång eller ytor som du vill återge.
* **`metadata`**: Anger hur HTML erbjudanden tillämpas. Det är en karta där nyckeln är ett omfång eller en yta, och värdet är ett objekt som innehåller tangenterna `selector` och `actionType`.
   * `selector`: En sträng som innehåller en CSS-väljare för var HTML ska användas.
   * `actionType`: Den åtgärd som ska utföras med HTML. Giltiga värden är `setHtml`, `replaceHtml` och `appendHtml`.
* **`viewName`**: Namnet på den vy som ska återges i ett enkelsidigt program. Visningsmeddelandena för dessa beslut cachelagras och kan inkluderas i ett efterföljande `sendEvent`-kommando med `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Använda offerter med taggtillägget Web SDK

Webbtaggtillägget för SDK som är ekvivalent med det här kommandot är åtgärden [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
