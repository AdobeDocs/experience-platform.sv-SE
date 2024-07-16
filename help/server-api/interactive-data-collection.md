---
title: Interaktiv datainsamling
description: Lär dig hur Adobe Experience Platform Edge Network Server API utför interaktiv datainsamling.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Interaktiv datainsamling

## Översikt {#overview}

Slutpunkter för interaktiv datainsamling tar emot en enda händelse och används när klienten förväntar sig att ett svar returneras av Adobe Experience Platform Edge Network-servern. Dessa slutpunkter kan också returnera innehåll från andra Edge Network-tjänster när datainsamling utförs.

>[!IMPORTANT]
>
>Slutpunkten `/interact` är främst avsedd att användas av SDK:er för Experience Platform. Den här slutpunkten kan ändras ytterligare och beteendet kan utvecklas utan föregående meddelande. Nya objekt kan till exempel läggas till i svarsnyttolasten i framtiden.

Serversvaret innehåller ett eller flera `Handle`-objekt, vilket visas nedan.

## Exempel på API-anrop

### API-format {#format}

```http
POST /ee/v2/interact
```

### Begäran {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
| `requestId` | `String` | Nej | Ange ett slumpmässigt klient-ID för korrelering av interna serverförfrågningar. Om inget anges genereras ett Edge Network och det returneras i svaret. |

### Svar {#response}

Ett lyckat svar returnerar HTTP-statusen `200 OK`, med ett eller flera `Handle`-objekt, beroende på vilka edge-tjänster i realtid som är aktiverade i datastream-konfigurationen.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
