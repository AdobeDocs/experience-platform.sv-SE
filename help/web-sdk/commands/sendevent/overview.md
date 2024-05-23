---
title: sendEvent
description: Skicka data till Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# `sendEvent`

The `sendEvent` kommandot är det primära sättet att skicka data till Adobe för att hämta personaliserat innehåll, identiteter och målgruppsmål. Använd [`xdm`](xdm.md) objekt för att skicka data som mappar till ditt Adobe Experience Platform-schema. Använd [`data`](data.md) objekt för att skicka data som inte är XDM. Du kan använda datastream-mapparen för att justera data inom det här objektet mot schemafält.

## Skicka händelsedata med tillägget Web SDK-tagg

Att skicka händelsedata utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Ange önskade fält och klicka på **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Skicka händelsedata med JavaScript-biblioteket för Web SDK

Kör `sendEvent` när du anropar den konfigurerade instansen av Web SDK. Se till att du ringer [`configure`](../configure/overview.md) innan du anropar `sendEvent` -kommando.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Svarsobjekt

Om du väljer att [hantera svar](../command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`propositions`**: En array med förslag som returneras av Edge Network. Exempel på förslag som återges automatiskt är flaggan `renderAttempted` ange till `true`.
* **`inferences`**: En array med härledningsobjekt som innehåller maskininlärningsinformation om den här användaren.
* **`destinations`**: En array med målobjekt som returneras av Edge Network.
