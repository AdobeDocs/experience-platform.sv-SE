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

Kommandot `sendEvent` är det primära sättet att skicka data till Adobe för att hämta personaliserat innehåll, identiteter och målgruppsmål. Använd objektet [`xdm`](xdm.md) för att skicka data som mappar till ditt Adobe Experience Platform-schema. Använd objektet [`data`](data.md) för att skicka data som inte är XDM. Du kan använda datastream-mapparen för att justera data inom det här objektet mot schemafält.

## Skicka händelsedata med tillägget Web SDK-tagg

Att skicka händelsedata utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Ange önskade fält, klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Skicka händelsedata med hjälp av JavaScript-biblioteket för Web SDK

Kör kommandot `sendEvent` när du anropar den konfigurerade instansen av Web SDK. Kontrollera att du anropar kommandot [`configure`](../configure/overview.md) innan du anropar kommandot `sendEvent`.

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

Om du bestämmer dig för att [hantera svar](../command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`propositions`**: En matris med förslag som returneras av Edge Network. Föreslag som återges automatiskt innehåller flaggan `renderAttempted` inställd på `true`.
* **`inferences`**: En array med härledningsobjekt som innehåller maskininlärningsinformation om den här användaren.
* **`destinations`**: En array med målobjekt som returneras av Edge Network.
