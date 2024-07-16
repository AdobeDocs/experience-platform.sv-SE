---
title: Icke-interaktiv datainsamling
description: Lär dig hur Adobe Experience Platform Edge Network Server API utför icke-interaktiv datainsamling.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---


# Icke-interaktiv datainsamling

## Översikt {#overview}

Icke-interaktiva slutpunkter för händelsedatainsamling används för att skicka flera händelser till datauppsättningar i Experience Platform eller andra kanaler.

Du bör skicka grupphändelser när slutanvändarhändelser köas lokalt under en kort tidsperiod (t.ex. när det inte finns någon nätverksanslutning).

Batchhändelser bör inte nödvändigtvis tillhöra samma slutanvändare, vilket innebär att händelser kan innehålla olika identiteter i sina `identityMap`-objekt.

## Exempel på icke-interaktiva API-anrop {#example}

### API-format {#api-format}

```http
POST /ee/v2/collect
```

### Begäran {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Ja | ID för datastream som används av datainsamlingsslutpunkten. |
| `requestId` | `String` | Nej | Ange ett ID för extern spårning av begäran. Om ingen anges genererar Edge Network en åt dig och returnerar den i svarstexten/sidhuvudena. |
| `silent` | `Boolean` | Nej | Valfri boolesk parameter som anger om Edge Network ska returnera ett `204 No Content`-svar med en tom nyttolast eller inte. Kritiska fel rapporteras med motsvarande HTTP-statuskod och nyttolast. |

### Svar {#response}

Ett lyckat svar returnerar en av följande statusvärden och en `requestID` om ingen har angetts i begäran.

* `202 Accepted` när begäran bearbetades,
* `204 No Content` när begäran bearbetades och parametern `silent` ställdes in på `true`;
* `400 Bad Request` när begäran inte var korrekt formaterad (t.ex. den obligatoriska primära identiteten hittades inte).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
