---
title: Spåra händelser med Adobe Experience Platform Web SDK
description: Lär dig spåra Adobe Experience Platform Web SDK-händelser.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 0%

---

# Spåra händelser

Om du vill skicka händelsedata till Adobe Experience Cloud använder du `sendEvent` -kommando. The `sendEvent` är det primära sättet att skicka data till [!DNL Experience Cloud]och hämta personaliserat innehåll, identiteter och målgruppsdestinationer.

Data som skickas till Adobe Experience Cloud kan delas in i två kategorier:

* XDM-data
* Ej XDM-data

## Skicka XDM-data

XDM-data är ett objekt vars innehåll och struktur matchar ett schema som du har skapat i Adobe Experience Platform. [Läs mer om hur du skapar ett schema.](../../xdm/tutorials/create-schema-ui.md)

Alla XDM-data som du vill ingå i dina analyser, personaliseringar, målgrupper eller mål ska skickas med `xdm` alternativ.


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
});
```

En viss tid kan förflyta mellan `sendEvent` kommandot körs och när data skickas till servern (om t.ex. Web SDK-biblioteket inte har lästs in fullständigt eller om samtycke ännu inte har tagits emot). Om du tänker ändra någon del av `xdm` efter att ha kört `sendEvent` rekommenderar vi att du klonar `xdm` object _före_ köra `sendEvent` -kommando. Exempel:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

I det här exemplet klonas datalagret genom att serialisera det till JSON och sedan deserialisera det. Därefter skickas det klonade resultatet till `sendEvent` -kommando. Om du gör det ser du till att `sendEvent` -kommandot har en fixering av datalagret som det var när `sendEvent` kommandot utfördes så att senare ändringar av det ursprungliga datalagret inte återspeglas i data som skickas till servern. Om du använder ett händelsestyrt datalager hanteras kloningen av dina data troligtvis redan automatiskt. Om du till exempel använder [Adobe-klientdatalager](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()` -metoden innehåller en beräknad, klonad ögonblicksbild av alla tidigare ändringar. Detta hanteras också automatiskt om du använder taggtillägget Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Det finns en gräns på 32 kB för de data som kan skickas i varje händelse i XDM-fältet.


## Skicka data som inte är XDM

Data som inte matchar ett XDM-schema ska skickas med `data` alternativ för `sendEvent` -kommando. Den här funktionen stöds i version 2.5.0 och senare av Web SDK.

Detta är användbart om du behöver uppdatera en Adobe Target-profil eller skicka Recommendations-attribut för mål. [Läs mer om dessa Target-funktioner.](../personalization/adobe-target/target-overview.md#single-profile-update)

I framtiden kommer du att kunna skicka hela datalagret under `data` och mappa det till XDM på serversidan.

**Så här skickar du attribut för profil och Recommendations till Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Inställning `eventType` {#event-types}

I XDM ExperienceEvent-scheman finns det ett valfritt `eventType` fält. Detta innehåller postens primära händelsetyp. Genom att ange en händelsetyp kan du skilja mellan olika händelser som du skickar in. XDM innehåller flera fördefinierade händelsetyper som du kan använda eller så skapar du alltid egna anpassade händelsetyper för dina användningsfall. Läs XDM-dokumentationen för en [lista med alla fördefinierade händelsetyper](../../xdm/classes/experienceevent.md#eventType).

De här händelsetyperna visas i en listruta om du använder taggtillägget eller så kan du alltid skicka dem utan taggar. De kan skickas in som en del av `xdm` alternativ.


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
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

Alternativt kan du `eventType` kan skickas till händelsekommandot med `type` alternativ. Bakom scenerna läggs detta till i XDM-data. Med `type` som ett alternativ som gör det enklare att ställa in `eventType` utan att behöva ändra XDM-nyttolasten.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Åsidosätta datauppsättnings-ID

>[!IMPORTANT]
>
>The `datasetId` som stöds av `sendEvent` kommandot har tagits bort. Om du vill åsidosätta ett datauppsättnings-ID använder du [konfigurationsåsidosättningar](../datastreams/overrides.md) i stället.

I vissa fall kanske du vill skicka en händelse till en annan datauppsättning än den som konfigurerats i konfigurationsgränssnittet. Därför måste du ange `datasetId` på `sendEvent` kommando:



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Lägga till identitetsinformation

Du kan även lägga till anpassad identitetsinformation till händelsen. Se [Hämtar Experience Cloud ID](../identity/overview.md).

## Använda API:t sendBeacon

Det kan vara svårt att skicka händelsedata precis innan webbsidans användare har navigerat. Om begäran tar för lång tid kan webbläsaren avbryta den. Vissa webbläsare har implementerat ett webbstandard-API som kallas `sendBeacon` för att göra det enklare att samla in data under denna tid. När du använder `sendBeacon`gör webbläsaren webbförfrågan i den globala webbläsarkontexten. Det innebär att webbläsaren gör beacon-begäran i bakgrunden och inte håller upp sidnavigeringen. Att berätta för Adobe Experience Platform [!DNL Web SDK] att använda `sendBeacon`, lägg till alternativet `"documentUnloading": true` till händelsekommandot.  Här är ett exempel:


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
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

Webbläsare har angett gränser för hur mycket data som kan skickas med `sendBeacon` samtidigt. I många webbläsare är gränsen 64 kB. Om webbläsaren avvisar händelsen eftersom nyttolasten är för stor, Adobe Experience Platform [!DNL Web SDK] använder sin normala transportmetod (till exempel hämta).

## Hantera svar från händelser

Om du vill hantera ett svar från en händelse kan du få ett meddelande om att åtgärden lyckades eller misslyckades enligt följande:


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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### The `result` object

The `sendEvent` returnerar ett löfte som lösts med ett `result` -objekt. The `result` -objektet innehåller följande egenskaper:

**förslag**: Personaliseringen erbjuder som besökaren är kvalificerad för. [Läs mer om offerter.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**beslut**: Den här egenskapen är föråldrad. Använd `propositions` i stället.

**mål**: Segment från Adobe Experience Platform som kan delas med externa personaliseringsplattformar, content management-system, annonsservrar och andra applikationer som körs på kundens webbplatser. [Läs mer om destinationer.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` är för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

## Ändra händelser globalt {#modifying-events-globally}

Om du vill lägga till, ta bort eller ändra fält från händelsen globalt kan du konfigurera en `onBeforeEventSend` återanrop.  Det här återanropet anropas varje gång en händelse skickas.  Det här återanropet skickas i ett händelseobjekt med ett `xdm` fält.  Ändra `content.xdm` för att ändra data som skickas med händelsen.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` fält anges i den här ordningen:

1. Värden som skickas som alternativ till händelsekommandot `alloy("sendEvent", { xdm: ... });`
2. Automatiskt insamlade värden.  (Se [Automatisk information](../data-collection/automatic-information.md).)
3. Ändringarna i `onBeforeEventSend` återanrop.

Några anteckningar om `onBeforeEventSend` callback:

* Händelse-XDM kan ändras under återanropet. När återanropet har returnerats skickas alla ändrade fält och värden för objekten content.xdm och content.data tillsammans med händelsen.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Om återanropet genererar ett undantag avbryts bearbetningen för händelsen och händelsen skickas inte.
* Om återanropet returnerar det booleska värdet för `false`, avbryts händelsebearbetningen utan något fel och händelsen skickas inte. Den här funktionen gör att vissa händelser enkelt kan ignoreras genom att händelsedata undersöks och returneras `false` om händelsen inte ska skickas.

   >[!NOTE]
   >Tänk på att undvika att returnera false vid den första händelsen på en sida. Om du returnerar false för den första händelsen kan det påverka personaliseringen negativt.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Alla andra returvärden än det booleska `false` gör att händelsen kan bearbetas och skickas efter återanropet.

* Händelser kan filtreras genom att undersöka händelsetypen (se [Händelsetyper](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Möjliga åtgärdbara fel

När du skickar en händelse kan ett fel inträffa om de data som skickas är för stora (över 32 kB för den fullständiga begäran). I det här fallet måste du minska mängden data som skickas.
