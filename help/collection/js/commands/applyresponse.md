---
title: applyResponse
description: Använd ett svar från Edge Network för att initiera Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

Med kommandot `applyResponse` kan du utföra olika åtgärder baserat på ett svar från Edge Network. Det används vanligtvis i hybriddistributioner där servern gör ett första anrop till Edge Network. Det här kommandot tar emot svaret från det anropet och initierar Web SDK i webbläsaren.

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

## Tillämpa svar med hjälp av taggtillägget Web SDK

Webbtaggtillägget för SDK som är ekvivalent med det här kommandot är åtgärden [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).
