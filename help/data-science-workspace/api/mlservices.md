---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Tjänster
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# MLServices

En MLService är en publicerad tränad modell som ger din organisation möjlighet att komma åt och återanvända tidigare utvecklade modeller. En viktig egenskap hos MLServices är möjligheten att automatisera kurser och poängsättning på schemalagd basis. Schemalagda kurser kan bidra till att bibehålla en modells effektivitet och exakthet, medan schemalagda kurser kan säkerställa att nya insikter genereras på ett konsekvent sätt.

Automatiserade utbildnings- och poängscheman definieras med en starttidsstämpel, en sluttidsstämpel och en frekvens som representeras som ett [cron-uttryck](https://en.wikipedia.org/wiki/Cron). Du kan definiera scheman när du [skapar en MLService](#create-an-mlservice) eller tillämpar dem genom att [uppdatera en befintlig MLService](#update-an-mlservice).

## Skapa en MLService {#create-an-mlservice}

Du kan skapa en MLService genom att utföra en begäran om POST och en nyttolast som anger ett namn för tjänsten och ett giltigt MLInstance-ID. Den MLInstance som används för att skapa en MLService behövs inte för att ha befintliga utbildningsexperter, men du kan välja att skapa MLService med en befintlig utbildad modell genom att ange motsvarande Experiment ID och ID för utbildningskörning.

**API-format**

```http
POST /mlServices
```

**Begäran**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet för MLService. Tjänsten som motsvarar denna MLService ärver det här värdet som ska visas i tjänstgalleriets användargränssnitt som tjänstens namn. |
| `description` | En valfri beskrivning för MLService. Tjänsten som motsvarar denna MLService ärver det här värdet som ska visas i användargränssnittet i tjänstgalleriet som tjänstens beskrivning. |
| `mlInstanceId` | Ett giltigt MLInstance-ID. |
| `trainingDataSetId` | Ett ID för utbildningsdatauppsättning som, om det anges, åsidosätter MLInstance standarddatauppsättning-ID. Om den MLInstance som används för att skapa MLService inte definierar en utbildningsdatauppsättning måste du ange ett lämpligt ID för utbildningsdatauppsättning. |
| `trainingExperimentId` | Ett Experiment-ID som du kan ange. Om det här värdet inte anges skapas även en ny expert med standardkonfigurationerna för MLInstance när du skapar MLService. |
| `trainingExperimentRunId` | Ett ID för utbildningskörning som du kan ange. Om det här värdet inte anges skapas och körs även en utbildningskörning med standardutbildningsparametrarna för MLInstance när du skapar MLService. |
| `trainingSchedule` | Ett schema för automatiserade kurser. Om den här egenskapen definieras kommer MLService automatiskt att utföra en schemalagd utbildning. |
| `trainingSchedule.startTime` | En tidsstämpel för vilken den schemalagda kursen börjar. |
| `trainingSchedule.endTime` | En tidsstämpel för vilken den schemalagda utbildningen kommer att avslutas. |
| `trainingSchedule.cron` | Ett cron-uttryck som definierar frekvensen av automatiska utbildningar. |
| `scoringSchedule` | Ett schema för automatiserad poängsättning. Om den här egenskapen definieras kommer MLService automatiskt att utföra en schemalagd poängsättning. |
| `scoringSchedule.startTime` | En tidsstämpel för vilken den schemalagda poängsättningen börjar. |
| `scoringSchedule.endTime` | En tidsstämpel för vilken den schemalagda poängsättningen avslutas. |
| `scoringSchedule.cron` | Ett cron-uttryck som definierar frekvensen för automatiserade poängkörningar. |

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller information om den nyligen skapade MLService, inklusive dess unika identifierare (`id`), test-ID för utbildning (`trainingExperimentId`), test-ID för poängsättning (`scoringExperimentId`) och datauppsättning-ID för inmatningsutbildning (`trainingDataSetId`).

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Hämta en lista med MLServices {#retrieve-a-list-of-mlservices}

Du kan hämta en lista över MLServices genom att utföra en enda begäran om GET. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

**API-format**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETER}` | En av de [tillgängliga frågeparametrarna](./appendix.md#query) som används för att filtrera resultaten. |
| `{VALUE}` | Värdet för föregående frågeparameter. |

**Begäran**

Följande begäran innehåller en fråga och hämtar en lista över MLServices som delar samma MLInstance-ID (`{MLINSTANCE_ID}`).

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista över MLServices och deras detaljer inklusive deras MLService-ID (`{MLSERVICE_ID}`), Experiment-ID för utbildning (`{TRAINING_ID}`), Experiment-ID för poängsättning (`{SCORING_ID}`) och datauppsättnings-ID för inmatningsutbildning (`{DATASET_ID}`).

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## Hämta en specifik MLService {#retrieve-a-specific-mlservice}

Du kan hämta information om en specifik Experiment genom att utföra en GET-begäran som innehåller det önskade MLService-ID:t i sökvägen för begäran.

**API-format**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Ett giltigt MLService-ID.

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den begärda MLService.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## Uppdatera en MLService {#update-an-mlservice}

Du kan uppdatera en befintlig MLService genom att skriva över dess egenskaper via en PUT-begäran som innehåller mål-MLService-ID:t i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP]
>
>För att denna PUT-begäran ska lyckas föreslår vi att du först utför en GET-begäran för att [hämta MLService via ID](#retrieve-a-specific-mlservice). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

**API-format**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: Ett giltigt MLService-ID.

**Begäran**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den uppdaterade informationen för MLService.

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## Ta bort en MLService

Du kan ta bort en enskild MLService genom att utföra en DELETE-begäran som innehåller mål-MLService-ID:t i sökvägen för begäran.

**API-format**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLSERVICE_ID}` | Ett giltigt MLService-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## Ta bort MLServices av MLInstance ID

Du kan ta bort alla MLServices som hör till en viss MLInstance genom att utföra en DELETE-begäran som anger ett MLInstance-ID som en frågeparameter.

**API-format**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLINSTANCE_ID}` | Ett giltigt MLInstance-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```
