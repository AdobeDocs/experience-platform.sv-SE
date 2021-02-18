---
title: Återge anpassat innehåll med Adobe Experience Platform Web SDK
description: Lär dig återge personaliserat innehåll med Adobe Experience Platform Web SDK.
keywords: personalisering;renderDecision;sendEvent;DecisionScopes;result.Decision;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Återge personaliserat innehåll

Adobe Experience Platform [!DNL Web SDK] stöder frågor om personaliseringslösningarna på Adobe, inklusive Adobe Target. Det finns två sätt att personalisera: hämta innehåll som kan återges automatiskt och innehåll som måste återges av utvecklaren. I SDK finns även funktioner för att [hantera flimmer](../personalization/manage-flicker.md).

## Återge innehåll automatiskt

SDK återger automatiskt anpassat innehåll när du skickar en händelse till servern och anger `renderDecisions` till `true` som ett alternativ för händelsen.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Återgivning av anpassat innehåll är asynkront, så det bör inte finnas några antaganden runt när ett visst innehåll är en del av sidan.

## Återge innehåll manuellt

Du kan begära att listan med beslut returneras som ett löfte för kommandot `sendEvent` genom att ange alternativet `decisionScopes`. Ett omfång är en sträng som låter personaliseringslösningen veta vilket beslut ni vill ha.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Detta returnerar en lista med beslut som ett JSON-objekt för varje beslut.

```json
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Om du använder [!DNL Target] blir omfattningar mBox på servern, men bara de begärs samtidigt i stället för individuellt. Den globala mbox skickas alltid.

### Hämta automatiskt innehåll

Om du vill att `result.decisions` ska inkludera de automatiskt återgivningsbara besluten och NOT har återge dem automatiskt, kan du ange `renderDecisions` till `false` och inkludera det särskilda omfånget `__view__`.
