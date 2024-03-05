---
title: applyPropositions
description: Återge utkast som redan har återgetts med sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# `applyPropositions`

The `applyPropositions` kan du återge utkast som redan har återgetts med [`sendEvent`](sendevent/overview.md) -kommando. Det här kommandot är användbart när du arbetar med enkelsidiga program där delar av sidan återges på nytt och eventuellt skriver över befintliga anpassningar av sidan.

Det här kommandot stöder följande fält:

* **Anbud**: En array med objekt som du vill återge.
* **Vynamn**: Namnet på den vy som ska återges. Visningsmeddelandena för de här besluten cachelagras och kan inkluderas i efterföljande `sendEvent` med kommandot `personalization.includePendingDisplayNotifications` alternativ.
* **Metadata**: Ett objekt som avgör hur erbjudanden från HTML kan tillämpas. Den innehåller följande egenskaper:
   * Omfång
   * Väljare
   * Åtgärdstyp

## Tillämpa förslag med hjälp av taggtillägget Web SDK

Föreslagen utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Apply propositions]**.
1. Ange önskade fält till höger.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Använda offerter med JavaScript-biblioteket för Web SDK

Kör `applyPropositions` när du anropar den konfigurerade instansen av Web SDK. Objektet som innehåller konfigurationsalternativ har stöd för följande fält:

* **`propositions`**: En array med objekt som du vill återge. Det här objektet används vanligtvis inte, eftersom `propositionScopes` fältet avgör vanligtvis vilka omfång eller ytor som du vill återge.
* **`metadata`**: Avgör hur erbjudanden från HTML tillämpas. Det är en karta där nyckeln är ett omfång eller en yta, och värdet är ett objekt som innehåller nycklarna `selector` och `actionType`.
   * `selector`: En sträng som innehåller en CSS-väljare för var HTML ska användas.
   * `actionType`: Den åtgärd som ska vidtas med HTML. Giltiga värden är `setHtml`, `replaceHtml`och `appendHtml`.
* **`viewName`**: Namnet på den vy som ska återges i ett enkelsidigt program. Visningsmeddelandena för de här besluten cachelagras och kan inkluderas i efterföljande `sendEvent` kommando använda `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
