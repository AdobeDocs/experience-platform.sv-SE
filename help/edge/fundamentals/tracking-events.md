---
title: Spåra händelser
seo-title: Spåra Adobe Experience Platform Web SDK-händelser
description: Lär dig spåra Experience Platform Web SDK-händelser
seo-description: Lär dig spåra Experience Platform Web SDK-händelser
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 0%

---


# Spåra händelser

Använd `sendEvent` kommandot om du vill skicka händelsedata till Adobe Experience Cloud. Kommandot `sendEvent` är det primära sättet att skicka data till [!DNL Experience Cloud]och hämta personaliserat innehåll, identiteter och målgruppsmål.

Data som skickas till Adobe Experience Cloud kan delas in i två kategorier:

* XDM-data
* Data som inte är XDM (stöds inte för närvarande)

## Skicka XDM-data

XDM-data är ett objekt vars innehåll och struktur matchar ett schema som du har skapat i Adobe Experience Platform. [Läs mer om hur du skapar ett schema.](../../xdm/tutorials/create-schema-ui.md)

Alla XDM-data som du vill ingå i dina analyser, personaliseringar, målgrupper eller mål ska skickas med `xdm` alternativet.


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

>[!NOTE]
>
>Det finns en gräns på 32 kB för de data som kan skickas i varje händelse i XDM-fältet.

### Skicka data som inte är XDM

För närvarande stöds inte sändning av data som inte matchar ett XDM-schema. Support planeras för ett framtida datum.

### Inställning `eventType`

I en XDM-upplevelsehändelse finns det ett valfritt `eventType` fält. Detta innehåller postens primära händelsetyp. Genom att ange en händelsetyp kan du skilja mellan olika händelser som du skickar in. XDM innehåller flera fördefinierade händelsetyper som du kan använda eller så skapar du alltid egna anpassade händelsetyper för dina användningsfall. Nedan visas en lista med alla fördefinierade händelsetyper som tillhandahålls av XDM. [Läs mer i den offentliga rapporten om XDM](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)


| **Händelsetyp:** | **Definition:** |
| ---------------------------------- | ------------ |
| advertising.completes | Anger om en mediefil som visas i tid har bevakats tills den är klar - det behöver inte innebära att användaren har tittat på hela videon. visningsprogrammet kunde ha hoppat över i förväg |
| advertising.timePlayed | Beskriver hur mycket tid en användare har lagt på en viss medieresurs med tidsangivelser |
| advertising.federated | Anger om en upplevelsehändelse har skapats via datafederation (datadelning mellan kunder) |
| advertising.clicks | Klicka på åtgärder i en annons |
| advertising.conversions | En fördefinierad åtgärd som utlöser en händelse för prestandautvärdering av en kund |
| advertising.firstQuartiles | En digital videoannons har spelat upp 25 % av sin längd med normal hastighet |
| advertising.impressions | Imponering(ar) av en annons till en slutanvändare som kan visas |
| advertising.midpoints | En digital videoannons har spelat upp 50 % av sin längd med normal hastighet |
| advertising.starts | En digital videoannons har börjat spela upp |
| advertising.thirdQuartiles | En digital videoannons har spelat upp 75 % av sin längd med normal hastighet |
| web.webpagedetails.pageViews | En webbsidas vy(er) har inträffat |
| web.webinteraction.linkClicks | Klicka på en webblänk har inträffat |
| commerce.checkouts | En åtgärd under en utcheckningsprocess för en produktlista kan vara mer än en utcheckningshändelse om det finns flera steg i en utcheckningsprocess. Om det finns flera steg används händelsetidsinformationen och sidan eller upplevelsen som refereras till för att identifiera det steg som enskilda händelser representerar i ordningen |
| commerce.productListAdds | En produkt läggs till i produktlistan. Exempel på en produkt som läggs till i en kundvagn |
| commerce.productListOpens | Initieringar av en ny produktlista. Exempel på en kundvagn skapas |
| commerce.productListRemovals | Borttagning av en produktpost från en produktlista. Exempel på en produkt som tas bort från en kundvagn |
| commerce.productListReopens | En produktlista som inte längre var tillgänglig (övergiven) har återaktiverats av användaren. Exempel via en ommarknadsföringsaktivitet |
| commerce.productListViews | En produktlistas vy(er) har inträffat |
| commerce.productViews | En eller flera produktvyer har skapats |
| commerce.purchases | En beställning har godkänts. Inköp är den enda nödvändiga åtgärden i en handelskonvertering. Köpet måste ha en produktlista som refereras |
| commerce.saveForLaters | Produktlistan sparas för framtida bruk. Exempel på en önskelista för en produkt |
| delivery.feedback | Feedback-händelser för leverans. Exempel på feedback-händelser för e-postleverans |


De här händelsetyperna visas i en listruta om du använder Adobe Experience Platform Launch-tillägget eller så kan du alltid skicka dem utan Experience Platform Launch. De kan skickas in som en del av `xdm` alternativet.


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

Alternativt kan `eventType` händelsen skickas till händelsekommandot med hjälp av `type` alternativet . Bakom scenerna läggs detta till i XDM-data. Med alternativet `type` som kan du enkelt ställa in `eventType` utan att behöva ändra XDM-nyttolasten.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Åsidosätta datauppsättnings-ID

I vissa fall kanske du vill skicka en händelse till en annan datauppsättning än den som konfigurerats i konfigurationsgränssnittet. Därför måste du ange alternativet `datasetId` för `sendEvent` kommandot:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Lägga till identitetsinformation

Du kan även lägga till anpassad identitetsinformation till händelsen. Se [Hämta Experience Cloud-ID](../identity/overview.md)

## Använda API:t sendBeacon

Det kan vara svårt att skicka händelsedata precis innan webbsidans användare har navigerat. Om begäran tar för lång tid kan webbläsaren avbryta den. Vissa webbläsare har implementerat ett webbläsar-API som anropas `sendBeacon` för att göra det enklare att samla in data under tiden. När webbläsaren använder `sendBeacon`den görs en webbförfrågan i det globala webbläsarsammanhanget. Det innebär att webbläsaren gör beacon-begäran i bakgrunden och inte håller upp sidnavigeringen. Om du vill ange att Adobe Experience Platform [!DNL Web SDK] ska använda `sendBeacon`lägger du till alternativet `"documentUnloading": true` i händelsekommandot.  Här är ett exempel:


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

Webbläsare har angett begränsningar för hur mycket data som kan skickas med `sendBeacon` samtidigt. I många webbläsare är gränsen 64 kB. Om webbläsaren avvisar händelsen eftersom nyttolasten är för stor återgår Adobe Experience Platform [!DNL Web SDK] till att använda sin normala transportmetod (till exempel hämta).

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

Om du vill lägga till, ta bort eller ändra fält från händelsen globalt, kan du konfigurera ett `onBeforeEventSend` återanrop.  Det här återanropet anropas varje gång en händelse skickas.  Det här återanropet skickas i ett händelseobjekt med ett `xdm` fält.  Ändra `event.xdm` om du vill ändra data som skickas i händelsen.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` fält anges i den här ordningen:

1. Värden som skickas som alternativ till händelsekommandot `alloy("sendEvent", { xdm: ... });`
2. Automatiskt insamlade värden.  (Se [Automatisk information](../data-collection/automatic-information.md).)
3. Ändringarna som har gjorts i `onBeforeEventSend` återanropet.

Om återanropet genererar ett undantag skickas händelsen fortfarande. `onBeforeEventSend` Inga av de ändringar som gjordes i återanropet tillämpas emellertid på den sista händelsen.

## Möjliga åtgärdbara fel

När du skickar en händelse kan ett fel inträffa om de data som skickas är för stora (över 32 kB för den fullständiga begäran). I det här fallet måste du minska mängden data som skickas.

När felsökning är aktiverat validerar servern synkront händelsedata som skickas mot det konfigurerade XDM-schemat. Om data inte matchar schemat returneras information om felmatchningen från servern och ett fel genereras. I det här fallet ändrar du data så att de matchar schemat. När felsökning inte är aktiverat validerar servern data asynkront och därför genereras inget motsvarande fel.
