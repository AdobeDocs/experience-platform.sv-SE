---
title: Återge personaliserat innehåll
seo-title: Adobe Experience Platform Web SDK Rendering personaliserat innehåll
description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK
seo-description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Översikt över personaliseringsalternativ

Adobe Experience Platform [!DNL Web SDK] stöder frågor om personaliseringslösningarna på Adobe, inklusive Adobe Target. Det finns två sätt att personalisera: hämta innehåll som kan återges automatiskt och innehåll som måste återges av utvecklaren. SDK har även funktioner för att [hantera flimmer](../../edge/solution-specific/target/flicker-management.md).

## Återge innehåll automatiskt

SDK återger automatiskt anpassat innehåll när du skickar en händelse till servern och anger `renderDecisions` den som ett alternativ `true` för händelsen.

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

Du kan begära att listan med beslut returneras som ett löfte för `sendEvent` kommandot genom att ange `decisionScopes` alternativet. Ett omfång är en sträng som låter personaliseringslösningen veta vilket beslut ni vill ha.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  })
```

Detta returnerar en lista med beslut som ett JSON-objekt för varje beslut.

```javascript
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
> Om du använder [!DNL Target]det blir omfattningar mBox på servern, men bara de begärs samtidigt i stället för individuellt. Den globala mbox skickas alltid.

### Hämta automatiskt innehåll

Om du vill `result.decisions` att inställningarna ska inkludera de automatiskt återgivningsbara besluten och INTE ha återge dem automatiskt, kan du ange `renderDecisions` till `false`och inkludera det speciella omfånget `__view__`.
