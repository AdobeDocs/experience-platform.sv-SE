---
title: sendEvent
description: Skicka data till Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

Kommandot `sendEvent` är det primära sättet att skicka data till Adobe. Dess svarsobjekt är det primära sättet att hämta personaliserat innehåll, identiteter och målgruppsmål. Använd objektet [`xdm`](xdm.md) för att skicka data som mappar till ditt Adobe Experience Platform-schema. Använd objektet [`data`](data.md) för att skicka data som inte är XDM. Nyttolasten när data skickas till Adobe har en maxgräns på 64 kB.

Kör kommandot `sendEvent` när du anropar den konfigurerade instansen av Web SDK. Kontrollera att du anropar kommandot [`configure`](../configure/overview.md) innan du anropar kommandot `sendEvent`.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Svarsobjekt

Om du bestämmer dig för att [hantera svar](../command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`propositions`**: En matris med förslag som returneras av Edge Network. Föreslag som återges automatiskt innehåller flaggan `renderAttempted` inställd på `true`.
* **`inferences`**: En array med härledningsobjekt som innehåller maskininlärningsinformation om den här användaren.
* **`destinations`**: En array med målobjekt som returneras av Edge Network.

## Skicka händelse med hjälp av taggtillägget Web SDK

Webbtaggtillägget för SDK är lika med det här kommandot som åtgärden [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).
