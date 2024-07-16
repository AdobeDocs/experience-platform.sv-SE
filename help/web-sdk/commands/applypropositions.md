---
title: applyPropositions
description: Återge utkast som redan har återgetts med sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# `applyPropositions`

Med kommandot `applyPropositions` kan du återge utkast som redan har återgetts med kommandot [`sendEvent`](sendevent/overview.md). Det här kommandot är användbart när du arbetar med enkelsidiga program där delar av sidan återges på nytt och eventuellt skriver över befintliga anpassningar av sidan.

Det här kommandot stöder följande fält:

* **Föreslag**: En array med objekt som du vill återge på nytt.
* **Visningsnamn**: Namnet på den vy som ska återges. Visningsmeddelandena för dessa beslut cachelagras och kan inkluderas i ett efterföljande `sendEvent`-kommando med alternativet `personalization.includePendingDisplayNotifications`.
* **Metadata**: Ett objekt som avgör hur erbjudanden från HTML kan tillämpas. Den innehåller följande egenskaper:
   * Omfång
   * Väljare
   * Åtgärdstyp

## Tillämpa förslag med hjälp av taggtillägget Web SDK

Föreslagen utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Apply propositions]**.
1. Ange önskade fält till höger.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Använda offerter med Web SDK JavaScript-biblioteket

Kör kommandot `applyPropositions` när du anropar den konfigurerade instansen av Web SDK. Objektet som innehåller konfigurationsalternativ har stöd för följande fält:

* **`propositions`**: En array med objekt som du vill återge igen. Det här objektet används vanligtvis inte, eftersom fältet `propositionScopes` vanligtvis avgör vilka omfång eller ytor som du vill återge.
* **`metadata`**: Anger hur erbjudanden från HTML tillämpas. Det är en karta där nyckeln är ett omfång eller en yta, och värdet är ett objekt som innehåller tangenterna `selector` och `actionType`.
   * `selector`: En sträng som innehåller en CSS-väljare för var HTML ska användas.
   * `actionType`: Den åtgärd som ska utföras med HTML. Giltiga värden är `setHtml`, `replaceHtml` och `appendHtml`.
* **`viewName`**: Namnet på den vy som ska återges i ett enkelsidigt program. Visningsmeddelandena för dessa beslut cachelagras och kan inkluderas i ett efterföljande `sendEvent`-kommando med `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
