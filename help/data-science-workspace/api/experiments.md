---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;experiments;sensei machine learning api
solution: Experience Platform
title: Experimentera
topic: Developer guide
description: Modellutveckling och utbildning sker på expertnivå, där en expert består av en MLInstance, utbildningar och poängprov.
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---


# Experimentera

Modellutveckling och utbildning sker på expertnivå, där en expert består av en MLInstance, utbildningar och poängprov.

## Skapa en expert {#create-an-experiment}

Du kan skapa en Experiment genom att utföra en POST-förfrågan och samtidigt ange ett namn och ett giltigt MLInstance-ID i nyttolasten för begäran.

>[!NOTE]
>
>Till skillnad från modellutbildning i användargränssnittet skapas och körs inte en kurskörning automatiskt när en expert skapas via ett explicit API-anrop.

**API-format**

```http
POST /experiments
```

**Begäran**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet för Experimenten. Utbildningen som motsvarar denna Experiment ärver det här värdet som ska visas i användargränssnittet som namn på utbildningskörningen. |
| `mlInstanceId` | Ett giltigt MLInstance-ID. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nyligen skapade experten, inklusive dess unika identifierare (`id`).

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Skapa och genomföra en utbildning eller ett poängprov {#experiment-training-scoring}

Du kan skapa utbildnings- eller poängkörningar genom att utföra en POST och ange ett giltigt test-ID och specificera körningsaktiviteten. Bedömningskörningar kan bara skapas om experten har en befintlig och framgångsrik utbildning. En utbildningskurs kommer att initiera modellutbildningsproceduren och om den slutförs utan fel genereras en tränad modell. När du genererar utbildade modeller ersätts alla befintliga modeller, så att en expert bara kan använda en enda tränad modell åt gången.

**API-format**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPERIMENT_ID}` | Ett giltigt test-ID. |

**Begäran**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `{TASK}` | Anger körningens aktivitet. Ange det här värdet som antingen `train` för utbildning, `score` för poängsättning eller `featurePipeline` för funktionsledning. |

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller information om den nyligen skapade körningen inklusive de ärvda standardutbildnings- eller poängparametrarna samt körningens unika ID (`{RUN_ID}`).

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Hämta en lista med experter

Du kan hämta en lista över experter som tillhör en viss MLInstance genom att utföra en enda GET-begäran och ange ett giltigt MLInstance-ID som en frågeparameter. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.


**API-format**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLINSTANCE_ID}` | Ange ett giltigt MLInstance-ID för att hämta en lista över experter som tillhör den aktuella MLInstance. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med experter som delar samma MLInstance-ID (`{MLINSTANCE_ID}`).

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## Hämta en specifik expert {#retrieve-specific}

Du kan hämta information om en specifik Experiment genom att utföra en GET-förfrågan som innehåller det önskade Experiment-ID:t i sökvägen för begäran.

**API-format**

```http
GET /experiments/{EXPERIMENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPERIMENT_ID}` | Ett giltigt test-ID. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den begärda experten.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Hämta en lista med Experimentkörningar

Du kan hämta en lista över utbildnings- eller poängsättningskörningar som tillhör en viss Experiment genom att utföra en enda GET-förfrågan och ange ett giltigt test-ID. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En fullständig lista över tillgängliga frågeparametrar finns i avsnittet i bilagan om [frågeparametrar för hämtning](./appendix.md#query)av resurser.

>[!NOTE]
>
>När du kombinerar flera frågeparametrar måste de avgränsas med et-tecken (&amp;).

**API-format**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPERIMENT_ID}` | Ett giltigt test-ID. |
| `{QUERY_PARAMETER}` | En av de [tillgängliga frågeparametrarna](./appendix.md#query) som används för att filtrera resultaten. |
| `{VALUE}` | Värdet för föregående frågeparameter. |

**Begäran**

Följande begäran innehåller en fråga och hämtar en lista över utbildningar som tillhör någon Experiment.

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller en lista över körningar och alla detaljer för dem, inklusive deras ID för Experiment Run (`{RUN_ID}`).

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Uppdatera en expert

Du kan uppdatera en befintlig Experiment genom att skriva över dess egenskaper via en PUT-begäran som innehåller målExperimentens ID i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP]
>
>För att PUT ska lyckas rekommenderar vi att du först utför en GET-förfrågan för att [hämta Experimentet via ID](#retrieve-specific). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

I följande exempel på API-anrop uppdateras en Experiments namn samtidigt som dessa egenskaper används från början:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API-format**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPERIMENT_ID}` | Ett giltigt test-ID. |

**Begäran**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den uppdaterade informationen för Experimenten.

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## Ta bort en expert

Du kan ta bort en enskild Experiment genom att utföra en DELETE-begäran som innehåller målExperimentens ID i sökvägen för begäran.

**API-format**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPERIMENT_ID}` | Ett giltigt test-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Ta bort experiment med MLInstance ID

Du kan ta bort alla experiment som tillhör en viss MLInstance genom att utföra en DELETE-begäran som innehåller MLInstance-ID:t som en frågeparameter.

**API-format**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | ---|
| `{MLINSTANCE_ID}` | Ett giltigt MLInstance-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiments successfully deleted"
}
```
