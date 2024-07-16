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

Med kommandot `applyResponse` kan du utföra olika åtgärder baserat på ett svar från Edge Network. Det används vanligtvis i hybriddistributioner där servern gör ett första anrop till Edge Network. Det här kommandot tar emot svaret från det anropet och initierar Web SDK i webbläsaren.

## Tillämpa svar med hjälp av taggtillägget Web SDK

Tillämpning av svar utförs som en åtgärd i en regel i tagggränssnittet för Adobe Experience Platform Data Collection.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Apply response]**.
1. Ange önskade fält till höger.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Tillämpa svar med hjälp av JavaScript-biblioteket för Web SDK

Kör kommandot `applyResponse` när du anropar den konfigurerade instansen av Web SDK. Objektet som innehåller konfigurationsalternativ har stöd för följande fält:

* **`renderDecisions`**: Ett booleskt värde som tvingar Web SDK att återge anpassat innehåll som kan återges automatiskt. Identisk med [`renderDecisions`](sendevent/renderdecisions.md) i kommandot [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: En mappning av strängrubriknamn till strängrubrikvärden.
* **`responseBody`**: Krävs. En JSON-svarstext från serveranropet till Edge Network.
* **`personalization.sendDisplayEvent`**: Ett booleskt värde som är identiskt med [`personalization.sendDisplayEvent`](sendevent/personalization.md) i kommandot `sendEvent`.

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

Om du bestämmer dig för att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`propositions`**: En matris med förslag som returneras av Edge Network. Föreslag som återges automatiskt innehåller flaggan `renderAttempted` inställd på `true`.
* **`inferences`**: En array med härledningsobjekt som innehåller maskininlärningsinformation om den här användaren.
* **`destinations`**: En array med målobjekt som returneras av Edge Network.
