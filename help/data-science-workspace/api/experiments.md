---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Experimentera
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Experimentera

Modellutveckling och utbildning sker på expertnivå, där en expert består av en MLInstance, utbildningar och poängprov.

## Skapa en expert

Du kan skapa en expert genom att utföra en POST-begäran och samtidigt ange ett namn och ett giltigt MLInstance-ID i nyttolasten för begäran.

>[!NOTE] Till skillnad från modellutbildning i användargränssnittet skapas och körs inte en kurskörning automatiskt när en expert skapas via ett explicit API-anrop.

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
        "mlInstanceId": "{MLINSTANCE_ID}"
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
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Skapa och genomföra en utbildning eller ett poängprov

Du kan skapa utbildnings- eller poängkörningar genom att utföra en POST-begäran och ange ett giltigt test-ID och specificera körningsaktiviteten. Bedömningskörningar kan bara skapas om experten har en befintlig och framgångsrik utbildning. En utbildningskurs kommer att initiera modellutbildningsproceduren och om den slutförs utan fel genereras en tränad modell. När du genererar utbildade modeller ersätts alla befintliga modeller, så att en expert bara kan använda en enda tränad modell åt gången.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
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
| `{TASK}` | Anger körningens aktivitet. Ange det här värdet som antingen `train` för utbildning, `score` för poängsättning eller `fp` för funktionsledning. |

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller information om den nyligen skapade körningen inklusive de ärvda standardutbildnings- eller poängparametrarna samt körningens unika ID (`{RUN_ID}`).

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

Du kan hämta en lista med experter som tillhör en viss MLInstance genom att utföra en GET-begäran och ange ett giltigt MLInstance-ID som en frågeparameter. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.


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
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
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
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

Du kan hämta information om en specifik expert genom att utföra en GET-begäran som innehåller det önskade Experimentets ID i sökvägen för begäran.

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den begärda experten.

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## Hämta en lista med Experimentkörningar

Du kan hämta en lista över utbildnings- eller poängsättningskörningar som tillhör en viss Experiment genom att utföra en GET-förfrågan och ange ett giltigt test-ID. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En fullständig lista över tillgängliga frågeparametrar finns i avsnittet i bilagan om [frågeparametrar för hämtning](./appendix.md#query)av resurser.

>[!NOTE] När du kombinerar flera frågeparametrar måste de avgränsas med et-tecken (&amp;).

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
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
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## Uppdatera en expert

Du kan uppdatera en befintlig Experiment genom att skriva över dess egenskaper via en PUT-begäran som inkluderar målExperimentens ID i den begärda sökvägen och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP] För att säkerställa att denna PUT-begäran lyckas föreslår vi att du först utför en GET-begäran för att [hämta Experiment via ID](#retrieve-specific). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

I följande exempel på API-anrop uppdateras en Experiments namn samtidigt som dessa egenskaper används från början:

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
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
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
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
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
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
