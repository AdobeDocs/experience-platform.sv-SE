---
title: Återge personaliserat innehåll
seo-title: Adobe Experience Platform Web SDK Rendering personaliserat innehåll
description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK
seo-description: Lär dig återge personaliserat innehåll med Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: bb3841da8a566105fde1b7ac78dccd79a7ea15d4

---


# (Beta) Översikt över personaliseringsalternativ

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform Web SDK stöder frågor om personaliseringslösningarna på Adobe inklusive Adobe Target. Det finns två sätt att personalisera: hämta innehåll som kan återges automatiskt och innehåll som måste återges av utvecklaren. SDK har även funktioner för att [hantera flimmer](managing-flicker.md).

## Återge innehåll automatiskt

SDK återger automatiskt anpassat innehåll när du skickar en händelse till servern och anger `renderDecisions` den som ett alternativ `true` för händelsen.

```javascript
alloy("event", {
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

Återgivningen av anpassat innehåll är asynkron, så det bör inte finnas några antaganden runt när ett visst innehåll är en del av sidan.

## Återge innehåll manuellt

Du kan begära att listan med beslut returneras som ett löfte för `event` kommandot med hjälp av `scopes`. Ett omfång är en sträng som låter personaliseringslösningen veta vilket beslut ni vill ha.

```javascript
alloy("event",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
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

{info}Om du använder Målomfattningar blir mBoxes på servern, är det bara de som blir alla förfrågningar på en gång i stället för individuellt. Den globala mbox skickas alltid.
{info}

### Hämta automatiskt innehåll

Om du vill `result.decisions` att den ska inkludera de automatiskt återgivningsbara besluten kan du ange false `renderDecisions` och inkludera det särskilda omfånget `__view__`
