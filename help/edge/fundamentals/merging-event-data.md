---
title: Sammanfoga händelsedata
seo-title: Sammanfoga händelsedata för Adobe Experience Platform Web SDK
description: Lär dig hur du sammanfogar händelsedata för Experience Platform Web SDK
seo-description: Lär dig hur du sammanfogar händelsedata för Experience Platform Web SDK
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# Sammanfoga händelsedata

>[!IMPORTANT]
>
>Den här funktionen är fortfarande under utveckling. Alla lösningar kan inte sammanfoga händelsedata enligt beskrivningen på den här sidan.

Ibland är inte alla data tillgängliga när en händelse inträffar. Du kanske vill hämta data som du _har_ så att de inte går förlorade om användaren till exempel stänger webbläsaren. Å andra sidan kan du även inkludera data som blir tillgängliga senare.

I sådana fall kan du sammanfoga data med tidigare händelser genom att skicka `eventMergeId` som ett alternativ till `event` kommandon enligt följande:

```javascript
alloy("sendEvent", {
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
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

Genom att skicka samma `eventMergeID` värde till båda händelsekommandona i det här exemplet utökas data i det andra händelsekommandot till data som tidigare skickats vid det första händelsekommandot. En post för varje händelsekommando skapas i [!DNL Experience Data Platform], men under rapporteringen förenas posterna med `eventMergeID` och visas som en enda händelse.

Om du skickar data om en viss händelse till tredjepartsleverantörer kan du även inkludera dessa data `eventMergeID` med dem. Om du senare väljer att importera tredjepartsdata till Adobe Experience Platform används de för att sammanfoga alla data som samlats in som ett resultat av den diskreta händelse som inträffade på din webbsida. `eventMergeID`

## Generera en `eventMergeID`

Värdet kan vara vilken sträng du vill, men kom ihåg att alla händelser som skickas med samma ID rapporteras som en enda händelse, så var försiktig med att framtvinga unika händelser när händelser inte ska sammanfogas. `eventMergeID` Om du vill att SDK ska generera ett unikt värde `eventMergeID` åt dig (enligt den vitt spridda [UID v4-specifikationen](https://www.ietf.org/rfc/rfc4122.txt)) kan du använda `createEventMergeId` kommandot för att göra det.

Precis som med alla kommandon returneras ett löfte eftersom du kan köra kommandot innan SDK-filen har lästs in. Löftet löses med ett unikt `eventMergeID` snarast möjligt. Du kan vänta på att löftet ska lösas innan du skickar data till servern enligt följande:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": results.eventMergeId
  });
});
```

Följ samma mönster om du vill ha åtkomst till `eventMergeID` av andra anledningar (till exempel för att skicka det till en tredjepartsleverantör):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Kommentarer i XDM-format

I händelsekommandot läggs `mergeId` det till i `xdm` nyttolasten.  Om du vill kan du skicka filen som en del av xdm-alternativet, så här: `mergeId`

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```
