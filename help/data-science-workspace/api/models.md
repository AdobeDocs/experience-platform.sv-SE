---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära topics;models;sensei machine learning api
solution: Experience Platform
title: API-slutpunkt för modeller
topic: Developer guide
description: En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---


# Modeller-slutpunkt

En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende.

## Hämta en lista med modeller

Du kan hämta en lista med modellinformation som tillhör alla modeller genom att utföra en enda GET-begäran till /models. Som standard sorteras den här listan från den äldsta modellen och resultatet begränsas till 25. Du kan välja att filtrera resultaten genom att ange vissa frågeparametrar. En lista över tillgängliga frågor finns i avsnittet i bilagan [frågeparametrar för hämtning](./appendix.md#query).

**API-format**

```http
GET /models
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om dina modeller, inklusive varje modells unika identifierare (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar modellen. |
| `modelArtifactUri` | En URI som anger var modellen lagras. URI:n avslutas med `name`-värdet för modellen. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |

## Hämta en specifik modell

Du kan hämta en lista med modellinformation som tillhör en viss modell genom att utföra en enda GET-begäran och ange ett giltigt modell-ID i sökvägen för begäran. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista över tillgängliga frågor finns i avsnittet i bilagan [frågeparametrar för hämtning](./appendix.md#query).

**API-format**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Identifieraren för den utbildade eller publicerade modellen. |
| `{EXPERIMENT_RUN_ID}` | Identifieraren för försökskörningen. |

**Begäran**

Följande begäran innehåller en fråga och hämtar en lista med tränade modeller som delar samma experimentRunID ({EXPERIMENT_RUN_ID}).

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om din modell, inklusive den unika identifieraren för modeller (`id`).

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar modellen. |
| `modelArtifactUri` | En URI som anger var modellen lagras. URI:n avslutas med `name`-värdet för modellen. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |

## Registrera en förgenererad modell {#register-a-model}

Du kan registrera en förgenererad modell genom att göra en POST-förfrågan till `/models`-slutpunkten. För att kunna registrera din modell måste egenskapsvärdena för `modelArtifact` och `model` inkluderas i förfrågningens innehåll.

**API-format**

```http
POST /models
```

**Begäran**

Följande POST innehåller de egenskapsvärden för `modelArtifact` och `model` som behövs. Se tabellen nedan för mer information om dessa värden.

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| Parameter | Beskrivning |
| --- | --- |
| `modelArtifact` | Platsen för den fullständiga modellartefakt du vill inkludera. |
| `model` | Formulärdata för modellobjektet som behöver skapas. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om din modell, inklusive den unika identifieraren för modeller (`id`).

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar modellen. |
| `modelArtifactUri` | En URI som anger var modellen lagras. URI:n avslutas med `id`-värdet för din modell. |

## Uppdatera en modell med ID

Du kan uppdatera en befintlig modell genom att skriva över dess egenskaper via en PUT-begäran som inkluderar målmodellens ID i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP]
>
>För att PUT ska lyckas rekommenderar vi att du först utför en GET-förfrågan om att hämta modellen efter ID. Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

**API-format**

```http
PUT /models/{MODEL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Identifieraren för den utbildade eller publicerade modellen. |

**Begäran**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den uppdaterade informationen för Experimenten.

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## Ta bort en modell med ID

Du kan ta bort en enskild modell genom att utföra en DELETE-begäran som innehåller målmodellens ID i sökvägen för begäran.

**API-format**

```http
DELETE /models/{MODEL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Identifieraren för den utbildade eller publicerade modellen. |

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller 200-status som bekräftar borttagningen av modellen.

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## Skapa en ny omkodning för en modell {#create-transcoded-model}

Transcoding är en direkt digital-till-digital-konvertering av en kodning till en annan. Du skapar en ny omkodning för en modell genom att ange de `{MODEL_ID}` och de `targetFormat` som du vill att de nya utdata ska vara i.

**API-format**

```http
POST /models/{MODEL_ID}/transcodings
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Identifieraren för den utbildade eller publicerade modellen. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett JSON-objekt med informationen om din omkodning. Detta inkluderar den unika identifieraren för transkodning (`id`) som används i [hämtning av en specifik trancoded Model](#retrieve-transcoded-model).

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## Hämta en lista över transkodningar för en modell {#retrieve-transcoded-model-list}

Du kan hämta en lista över transkodningar som har utförts på en modell genom att utföra en GET-begäran med din `{MODEL_ID}`.

**API-format**

```http
GET /models/{MODEL_ID}/transcodings
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Identifieraren för den utbildade eller publicerade modellen. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett json-objekt med en lista över varje omkodning som har utförts i modellen. Varje omkodad modell får en unik identifierare (`id`).

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## Hämta en specifik omkodad modell {#retrieve-transcoded-model}

Du kan hämta en viss omkodad modell genom att utföra en GET-förfrågan med ditt `{MODEL_ID}` och ID:t för en omkodad modell.

**API-format**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MODEL_ID}` | Unik identifierare för en utbildad eller publicerad modell. |
| `{TRANSCODING_ID}` | Den unika identifieraren för en omkodad modell. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller ett JSON-objekt med data från den omkodade modellen.

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```


