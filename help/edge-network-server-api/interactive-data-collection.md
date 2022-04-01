---
title: Interaktiv datainsamling
description: Läs om hur API:t för Adobe Experience Platform Edge Network Server utför interaktiv datainsamling
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: datainsamling;samling;upplevelseplattform kantnätverk;api;interaktiv datainsamling
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---


# Interaktiv datainsamling

## Översikt {#overview}

Slutpunkter för interaktiv datainsamling tar emot en enda händelse och används när klienten förväntar sig att ett svar returneras av Adobe Experience Platform Edge Network-servern. Dessa slutpunkter kan också returnera innehåll från andra Experience Edge-tjänster när du samlar in data.

Serversvaret innehåller en eller flera `Handle` objekt, enligt nedan.

## Exempel på API-anrop

### API-format {#format}

```http
POST /ee/v2/interact
```

### Begäran {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja. | Datastream-ID. |
| `requestId` | `String` | Nej | Ange ett slumpmässigt klient-ID för korrelerande interna serverförfrågningar. Om inget anges genereras ett Edge-nätverk och returneras som svar. |

### Svar {#response}

Ett godkänt svar returnerar HTTP-status `200 OK`, med en eller flera `Handle` objekt, beroende på vilka edge-tjänster i realtid som är aktiverade i datastream-konfigurationen.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
