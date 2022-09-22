---
title: Dataförberedelse för datainsamling
description: Lär dig hur du mappar data till ett XDM-händelseschema (Experience Data Model) när du konfigurerar ett datastam för Adobe Experience Platform Web och Mobile SDK.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# Dataförberedelse för datainsamling

Data Prep är en Adobe Experience Platform-tjänst som gör att du kan mappa, omvandla och validera data till och från [Experience Data Model (XDM)](../../xdm/home.md). När en plattform konfigureras [datastream](./overview.md)kan du använda Data Prep-funktioner för att mappa dina källdata till XDM när du skickar dem till Platform Edge Network.

>[!NOTE]
>
>Mer utförlig vägledning om alla funktioner för dataförberedelser, inklusive omformningsfunktioner för beräknade fält, finns i följande dokumentation:
>
>* [Översikt över datapreflight](../../data-prep/home.md)
>* [Funktioner för datapersonmappning](../../data-prep/functions.md)
>* [Hantera dataformat med Data Prep](../../data-prep/data-handling.md)


Den här guiden beskriver hur du mappar data i användargränssnittet för datainsamling. Om du vill följa med i stegen börjar du med att skapa en datastream upp till (och inkludera) [grundläggande konfigurationssteg](./overview.md#create).

En snabb demonstration av datainsamlingsprocessen finns i följande video:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Select data] {#select-data}

Välj **[!UICONTROL Save and Add Mapping]** när du har slutfört den grundläggande konfigurationen för ett datastream, och **[!UICONTROL Select data]** visas. Härifrån måste du ange ett exempel på ett JSON-objekt som representerar strukturen för de data som du planerar att skicka till Platform.

Om du vill hämta egenskaper direkt från datalagret måste JSON-objektet ha en enda rotegenskap `data`. Underegenskaperna för `data` objektet ska sedan konstrueras på ett sätt som mappar till datalagrets egenskaper som du vill hämta. Markera avsnittet nedan om du vill visa ett exempel på ett korrekt formaterat JSON-objekt med ett `data` rot.

+++Exempel på JSON-fil med `data` root

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Om du vill hämta egenskaper från ett XDM-objektdataelement gäller samma regler för JSON-objektet, men rotegenskapen måste anges som `xdm` i stället. Markera avsnittet nedan om du vill visa ett exempel på ett korrekt formaterat JSON-objekt med ett `xdm` rot.

+++Exempel på JSON-fil med `xdm` root

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

Du kan välja att överföra objektet som en fil eller klistra in raw-objektet i den angivna textrutan i stället. Om JSON är giltig visas ett förhandsgranskningsschema i den högra panelen. Välj **[!UICONTROL Next]** för att fortsätta.

![JSON-exempel på förväntade inkommande data](../images/datastreams/data-prep/select-data.png)

## [!UICONTROL Mapping]

The **[!UICONTROL Mapping]** visas så att du kan mappa fälten i källdata till målhändelseschemats fält i Platform. Här kan du konfigurera mappningen på två sätt:

* [Skapa nya mappningsregler](#create-mapping) för denna datastream genom en manuell process.
* [Importera mappningsregler](#import-mapping) från en befintlig datastream.

### Skapa en ny mappning {#create-mapping}

För att komma igång väljer du **[!UICONTROL Add new mapping]** för att skapa en ny mappningsrad.

![Lägga till en ny mappning](../images/datastreams/data-prep/add-new-mapping.png)

Välj källikon (![Källikon](../images/datastreams/data-prep/source-icon.png)) och i den dialogruta som visas väljer du det källfält som du vill mappa på den angivna arbetsytan. När du har valt ett fält använder du **[!UICONTROL Select]** för att fortsätta

![Markera fältet som ska mappas i källschemat](../images/datastreams/data-prep/source-mapping.png)

Välj sedan schemaikonen (![Schemaikon](../images/datastreams/data-prep/schema-icon.png)) för att öppna en liknande dialogruta för målhändelseschemat. Välj det fält som du vill mappa data till innan du bekräftar med **[!UICONTROL Select]**.

![Markera fältet som ska mappas i målschemat](../images/datastreams/data-prep/target-mapping.png)

Mappningssidan visas igen med den ifyllda fältmappningen. The **[!UICONTROL Mapping progress]** avsnittsuppdateringar för att återspegla det totala antalet fält som har mappats.

![Fältet har mappats med förloppet speglat](../images/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Om du vill mappa en array med objekt (i källfältet) till en array med olika objekt (i målfältet) lägger du till `[*]` efter arraynamnet i käll- och målfältssökvägarna, vilket visas nedan.
>
>![Arrayobjektsmappning](../images/datastreams/data-prep/array-object-mapping.png)

### Importera befintliga mappningsregler {#import-mapping}

Om du tidigare har skapat ett datastream kan du återanvända dess konfigurerade mappningsregler för ett nytt datastream.

>[!WARNING]
>
>Om du importerar mappningsregler från en annan datastream skrivs eventuella fältmappningar som du har lagt till före importen över.

Börja genom att välja **[!UICONTROL Import Mapping]**.

![Bilden visar [!UICONTROL Import Mapping] knappen markeras](../images/datastreams/data-prep/import-mapping-button.png)

I den dialogruta som visas markerar du datastream vars mappningsregler du vill importera. När du har valt datastream väljer du **[!UICONTROL Preview]**.

![Bild som visar ett befintligt datastream som markeras](../images/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Datastreams kan bara importeras inom samma [sandlåda](../../sandboxes/home.md). Du kan alltså inte importera ett datastam från en sandlåda till en annan.

På nästa skärm visas en förhandsvisning av de sparade mappningsreglerna för det valda datastream. Kontrollera att de visade mappningarna är vad du förväntar dig och välj sedan **[!UICONTROL Import]** för att bekräfta och lägga till mappningarna i den nya datastream.

![Bild som visar mappningsreglerna som ska importeras](../images/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Om några källfält i de importerade mappningsreglerna inte ingår i JSON-exempeldata som du använder [tidigare](#select-data)kommer dessa fältkopplingar inte att inkluderas i importen.

### Slutför mappningen

Följ stegen ovan för att mappa resten av fälten till målschemat. Även om du inte behöver mappa alla tillgängliga källfält, måste alla fält i målschemat som har angetts som obligatoriska mappas för att det här steget ska kunna slutföras. The **[!UICONTROL Required fields]** anger hur många obligatoriska fält som ännu inte har mappats i den aktuella konfigurationen.

När antalet obligatoriska fält har nått noll och du är nöjd med mappningen väljer du **[!UICONTROL Save]** för att slutföra ändringarna.

![Mappningen är klar](../images/datastreams/data-prep/mapping-complete.png)

## Nästa steg

I den här guiden beskrivs hur du mappar data till XDM när du konfigurerar ett datastam i användargränssnittet för datainsamling. Om du följer den allmänna datastreams-självstudiekursen kan du nu gå tillbaka till steget [visa information om dataström](./overview.md).
