---
title: Interagera med Adobe Analytics
description: Lär dig hur du använder API:t för Edge Network Server för att interagera med Adobe Analytics
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: datainsamling, Utlopp. Analyser. Adobe Experience Platform Edge Network API;analytics
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 396dc8d861f0e699a76aa367fc07fe62be804cc5
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Interagera med Adobe Analytics

## Översikt {#overview}

Adobe Analytics datainsamling fungerar genom att översätta XDM-data till ett format som Adobe Analytics kan förstå. Flera XDM-fält är [automatiskt mappad](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) till analysvariabler.

Du kan också [mappa XDM-värden manuellt](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) till äldre analysvariabler.

Om du vill att Adobe Analytics ska kunna ta emot data från Server-API:t måste du [konfigurera ditt datastream](../edge/datastreams/overview.md#adobe-analytics-settings) om du vill vidarebefordra händelser till Adobe Analytics genom att ange rapportsvitens ID på konfigurationssidan för datastream.

![Adobe Analytics DataStream-konfiguration](assets/analytics-datastream.png)

## Interagera med Adobe Analytics {#interacting-analytics}

### API-format {#format}

```http
POST https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Begäran {#request}

Exemplet nedan innehåller flera automatiskt mappade värden från `_experience.analytics` fältgrupp. Den innehåller även JSON-baserade datalager. Dessa datalager kan inte mappas automatiskt, men det går att använda [Dataförberedelse för datainsamling](../edge/datastreams/data-prep.md) för att mappa dessa värden till ett schema som innehåller fältgrupper som refereras ovan.

Alla värden som användarna mappar till dessa fält mappas automatiskt till rätt Analytics-värden, som om de ingick i API-begäran.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### Svar {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
