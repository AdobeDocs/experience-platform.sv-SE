---
title: applyResponse
description: Använd ett svar från Edge Network för att initiera Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# `applyResponse`

The `applyResponse` kan du utföra olika åtgärder baserat på ett svar från Edge Network. Det används vanligtvis i hybriddistributioner där servern gör ett första anrop till Edge Network. Det här kommandot tar emot svaret från det anropet och initierar Web SDK i webbläsaren.

## Tillämpa svar med hjälp av taggtillägget Web SDK

Tillämpning av svar utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Apply response]**.
1. Ange önskade fält till höger.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Tillämpa svar med JavaScript-biblioteket för Web SDK

Kör `applyResponse` när du anropar den konfigurerade instansen av Web SDK. Objektet som innehåller konfigurationsalternativ har stöd för följande fält:

* **`renderDecisions`**: Ett booleskt värde som tvingar Web SDK att återge anpassat innehåll som kan återges automatiskt. Identisk med [`renderDecisions`](sendevent/renderdecisions.md) i [`sendEvent`](sendevent/overview.md) -kommando.
* **`responseHeaders`**: En mappning av strängrubriknamn till strängrubrikvärden.
* **`responseBody`**: Obligatoriskt. En JSON-svarstext från serveranropet till Edge Network.
* **`personalization.sendDisplayEvent`**: Ett booleskt värde som fungerar likadant som [`personalization.sendDisplayEvent`](sendevent/personalization.md) i `sendEvent` -kommando.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Svarsobjekt

Om du väljer att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`propositions`**: En array med förslag som returneras av Edge Network. Exempel på förslag som återges automatiskt är flaggan `renderAttempted` ange till `true`.
* **`inferences`**: En array med härledningsobjekt som innehåller maskininlärningsinformation om den här användaren.
* **`destinations`**: En array med målobjekt som returneras av Edge Network.
