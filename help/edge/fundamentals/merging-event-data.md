---
title: Sammanfoga händelsedata
seo-title: Sammanfoga händelsedata för Adobe Experience Platform Web SDK
description: Lär dig hur du sammanfogar händelsedata för Experience Platform Web SDK
seo-description: Lär dig hur du sammanfogar händelsedata för Experience Platform Web SDK
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Sammanfoga händelsedata

>[!IMPORTANT]
>
>Den här funktionen är fortfarande under utveckling. Alla lösningar kan inte sammanfoga händelsedata enligt beskrivningen på den här sidan.

Ibland är inte alla data tillgängliga när en händelse inträffar. Du kanske vill samla in data som du har så att de inte går förlorade om användaren till exempel stänger webbläsaren. Å andra sidan kan du även inkludera data som blir tillgängliga senare.

I sådana fall kan du sammanfoga data med tidigare händelser genom att skicka `mergeId` som ett alternativ till `event` kommandon enligt följande:

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
  },
  "mergeId": "ABC123"
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
  },
  "mergeId": "ABC123"
});
```

Genom att skicka samma värde för alternativet till båda händelsekommandona i det här exemplet, utökas data i det andra händelsekommandot till data som tidigare skickats vid det första händelsekommandot. `mergeId` En post för varje händelsekommando skapas i [!DNL Experience Data Platform], men under rapporteringen sammanfogas posterna med händelsesammanfognings-ID:t och visas som en enda händelse.

Om du skickar data om en viss händelse till tredjepartsleverantörer kan du även inkludera samma ID för händelsesammanfogning med dessa data. Om du senare väljer att importera data från tredje part till Adobe Experience Platform, kommer ID:t för händelsesammanfogning att användas för att sammanfoga alla data som samlats in som ett resultat av den diskreta händelsen som inträffade på din webbsida.

## Generera ett ID för händelsesammanfogning

Händelsens sammanfognings-ID kan vara vilken sträng som helst, men kom ihåg att alla händelser som skickas med samma ID rapporteras som en enda händelse, så var försiktig med att framtvinga unika händelser när händelser inte ska sammanfogas. Om du vill att SDK ska generera ett unikt ID för händelsesammanfogning åt dig (i enlighet med den allmänt använda [UID v4-specifikationen](https://www.ietf.org/rfc/rfc4122.txt)) kan du använda `createEventMergeId` kommandot för att göra det.

Precis som med alla kommandon returneras ett löfte eftersom du kan köra kommandot innan SDK-filen har lästs in. Löftet löses med ett unikt ID för händelsesammanfogning så snart som möjligt. Du kan vänta på att löftet ska lösas innan du skickar data till servern enligt följande:

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
    },
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
    },
    "mergeId": results.eventMergeId
  });
});
```

Följ samma mönster om du av andra anledningar vill ha åtkomst till händelsesammanfognings-ID (till exempel för att skicka det till en tredjepartsleverantör):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Kommentarer i XDM-format

I händelsekommandot läggs ID:t för händelsesammanfogning till i nyttolasten på rätt plats för din räkning. `xdm`  Om du vill kan du istället skicka händelsens sammanfognings-ID som en del av `xdm` alternativet, enligt följande:

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

När du lägger till händelsesammanfognings-ID:t direkt till `xdm` objektet, ska du lägga märke till att namnet `eventMergeID` används i stället för `mergeId`.
