---
title: Spåra händelser med Adobe Experience Platform Web SDK
description: Lär dig spåra Adobe Experience Platform Web SDK-händelser.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 53a14b2b7d7ca8bdd278f2aeec2c2e8a30fdac7b
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# Spåra händelser

Om du vill skicka händelsedata till Adobe Experience Cloud använder du kommandot `sendEvent`. Kommandot `sendEvent` är det primära sättet att skicka data till [!DNL Experience Cloud] och att hämta personaliserat innehåll, identiteter och målgruppsmål.

Data som skickas till Adobe Experience Cloud kan delas in i två kategorier:

* XDM-data
* Ej XDM-data

## Skicka XDM-data

XDM-data är ett objekt vars innehåll och struktur matchar ett schema som du har skapat i Adobe Experience Platform. [Läs mer om hur du skapar ett schema.](../../xdm/tutorials/create-schema-ui.md)

Alla XDM-data som du vill ingå i dina analyser, personaliseringar, målgrupper eller mål ska skickas med alternativet `xdm`.


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

Det kan gå en stund mellan när kommandot `sendEvent` körs och när data skickas till servern (till exempel om Web SDK-biblioteket inte har lästs in fullständigt eller om samtycke ännu inte har tagits emot). Om du tänker ändra någon del av `xdm`-objektet efter att du har kört kommandot `sendEvent` rekommenderar vi att du klonar `xdm`-objektet _innan du_ kör kommandot `sendEvent`. Exempel:

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

I det här exemplet klonas datalagret genom att serialisera det till JSON och sedan deserialisera det. Sedan skickas det klonade resultatet till kommandot `sendEvent`. Om du gör det ser du till att kommandot `sendEvent` har en ögonblicksbild av datalagret som det var när kommandot `sendEvent` kördes så att senare ändringar av det ursprungliga datalagret inte återspeglas i data som skickas till servern. Om du använder ett händelsestyrt datalager hanteras kloningen av dina data troligtvis redan automatiskt. Om du till exempel använder [Adobe-klientdatalagret](https://github.com/adobe/adobe-client-data-layer/wiki), ger metoden `getState()` en beräknad, klonad ögonblicksbild av alla tidigare ändringar. Detta hanteras också automatiskt om du använder taggtillägget Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Det finns en gräns på 32 kB för de data som kan skickas i varje händelse i XDM-fältet.


## Skicka data som inte är XDM

Data som inte matchar ett XDM-schema ska skickas med alternativet `data` för kommandot `sendEvent`. Den här funktionen stöds i version 2.5.0 och senare av Web SDK.

Detta är användbart om du behöver uppdatera en Adobe Target-profil eller skicka Recommendations-attribut för mål. [Läs mer om dessa Target-funktioner.](../personalization/adobe-target/target-overview.md#single-profile-update)

I framtiden kommer du att kunna skicka hela datalagret under alternativet `data` och mappa det till XDM-serversidan.

**Så här skickar du attribut för profil och Recommendations till Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### Inställning `eventType` {#event-types}

I XDM ExperienceEvent-scheman finns det ett valfritt `eventType`-fält. Detta innehåller postens primära händelsetyp. Genom att ange en händelsetyp kan du skilja mellan olika händelser som du skickar in. XDM innehåller flera fördefinierade händelsetyper som du kan använda eller så skapar du alltid egna anpassade händelsetyper för dina användningsfall. I XDM-dokumentationen finns en [lista över alla fördefinierade händelsetyper](../../xdm/classes/experienceevent.md#eventType).

De här händelsetyperna visas i en listruta om du använder taggtillägget eller så kan du alltid skicka dem utan taggar. De kan skickas som en del av `xdm`-alternativet.


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

Alternativt kan du skicka `eventType` till händelsekommandot med alternativet `type`. Bakom scenerna läggs detta till i XDM-data. Om du har `type` som ett alternativ kan du enkelt ställa in `eventType` utan att behöva ändra XDM-nyttolasten.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Åsidosätta datauppsättnings-ID

I vissa fall kanske du vill skicka en händelse till en annan datauppsättning än den som konfigurerats i konfigurationsgränssnittet. Därför måste du ange alternativet `datasetId` för kommandot `sendEvent`:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Lägga till identitetsinformation

Du kan även lägga till anpassad identitetsinformation till händelsen. Se [Hämta Experience Cloud ID](../identity/overview.md).

## Använda API:t sendBeacon

Det kan vara svårt att skicka händelsedata precis innan webbsidans användare har navigerat. Om begäran tar för lång tid kan webbläsaren avbryta den. Vissa webbläsare har implementerat ett webbstandard-API med namnet `sendBeacon` så att data enklare kan samlas in under den här tiden. När du använder `sendBeacon` gör webbläsaren en webbförfrågan i den globala webbläsarkontexten. Det innebär att webbläsaren gör beacon-begäran i bakgrunden och inte håller upp sidnavigeringen. Om du vill att Adobe Experience Platform [!DNL Web SDK] ska använda `sendBeacon` lägger du till alternativet `"documentUnloading": true` i händelsekommandot.  Här är ett exempel:


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

Webbläsare har angett gränser för hur mycket data som kan skickas med `sendBeacon` samtidigt. I många webbläsare är gränsen 64 kB. Om webbläsaren avvisar händelsen eftersom nyttolasten är för stor återgår Adobe Experience Platform [!DNL Web SDK] till att använda sin normala transportmetod (till exempel hämta).

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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Ändra händelser globalt {#modifying-events-globally}

Om du vill lägga till, ta bort eller ändra fält från händelsen globalt kan du konfigurera ett `onBeforeEventSend`-återanrop.  Det här återanropet anropas varje gång en händelse skickas.  Det här återanropet skickas i ett händelseobjekt med ett `xdm`-fält.  Ändra `content.xdm` om du vill ändra data som skickas med händelsen.


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
3. Ändringarna som gjorts i `onBeforeEventSend`-återanropet.

Några anteckningar om `onBeforeEventSend`-återanropet:

* Händelse-XDM kan ändras under återanropet. När återanropet har returnerats ändras fälten och värdena för
objekten content.xdm och content.data skickas tillsammans med händelsen.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Om återanropet genererar ett undantag avbryts bearbetningen för händelsen och händelsen skickas inte.
* Om återanropet returnerar det booleska värdet `false` avbryts händelsebearbetningen,
utan fel och händelsen skickas inte. Den här funktionen gör att vissa händelser enkelt kan ignoreras av
undersöker händelsedata och returnerar `false` om händelsen inte ska skickas.

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

* Händelser kan filtreras genom att undersöka händelsetypen (Se [Händelsetyper](#event-types).):

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
