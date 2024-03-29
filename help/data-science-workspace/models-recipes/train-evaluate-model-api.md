---
keywords: Experience Platform;utbilda och utvärdera;Data Science Workspace;populära ämnen;Sensei Machine Learning API
solution: Experience Platform
title: Utbildning och utvärdering av en modell med Sensei Machine Learning API
type: Tutorial
description: I den här självstudiekursen visas hur du skapar, utbilda och utvärderar en modell med API-anrop för Sensei Machine Learning.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Tåla och utvärdera en modell med [!DNL Sensei Machine Learning] API


I den här självstudiekursen visas hur du skapar, utbilda och utvärderar en modell med API-anrop. Se [det här dokumentet](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) för en detaljerad lista över API-dokumentation.

## Förutsättningar

Följ [Importera en paketerad mottagare med API:t](./import-packaged-recipe-api.md) för att skapa en motor, som krävs för att utbilda och utvärdera en modell med API:t.

Följ [Självstudiekurs om autentisering med Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en) för att börja göra API-anrop.

Från självstudiekursen bör du nu ha följande värden:

- `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.
- `{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.

- Länka till en dockningsbild av en intelligent tjänst

## API-arbetsflöde

Vi kommer att konsumera API:erna för att skapa en Experimentrunda för utbildning. I den här självstudiekursen kommer vi att fokusera på slutpunkterna för motorer, MLInstances och Experiments. I följande diagram visas relationen mellan de tre versionerna och även en introduktion till en Run och en Model.

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>Termerna&quot;Engine&quot;,&quot;MLInstance&quot;,&quot;MLService&quot;,&quot;Experiment&quot; och&quot;Model&quot; kallas olika termer i användargränssnittet. Om du kommer från gränssnittet mappas skillnaderna i följande tabell.

| Användargränssnittsterm | API-term |
| --- | --- |
| Recipe | Motor |
| Modell | MLInstance |
| Utbildningsprogram | Experimentera |
| Tjänst | MLService |

### Skapa en MLInstance

Du kan skapa en MLInstance med följande begäran. Du kommer att använda `{ENGINE_ID}` som returnerades när en motor skapades från [Importera en paketerad mottagare med API:t](./import-packaged-recipe-ui.md) självstudiekurs.

**Begäran**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Konfigurationen av vår MLInstance. Exemplet vi använder i vår självstudiekurs visas här:

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>I `{JSON_PAYLOAD}`definierar vi parametrar för utbildning och poängsättning i `tasks` array. The `{ENGINE_ID}` är ID:t för den motor som du vill använda och `tag` -fältet är en valfri parameter som används för att identifiera instansen.

Svaret innehåller `{INSTANCE_ID}` som representerar den skapade MLInstance-instansen. Flera MLInstances-modeller med olika konfigurationer kan skapas.

**Svar**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`: Detta ID representerar motorn som MLInstance skapas under.\
`{INSTANCE_ID}`: Det ID som representerar MLInstance.

### Skapa en expert

En datavetare använder en expert för att komma fram till en högpresterande modell under utbildningen. Det finns många olika experimentalternativ, till exempel ändrade datauppsättningar, funktioner, inlärningsparametrar och maskinvara. Följande är ett exempel på hur du skapar en expert.

**Begäran**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Experimentera med objekt som skapas. Exemplet vi använder i vår självstudiekurs visas här:

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`: Det ID som representerar MLInstance.

Svaret från experten ser ut så här.

**Svar**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`: Det ID som representerar den expert du just har skapat.
`{INSTANCE_ID}`: Det ID som representerar MLInstance.

### Skapa en schemalagd övning för utbildning

Schemalagda experiment används så att vi inte behöver skapa varje enskild Experiment Runs via ett API-anrop. I stället tillhandahåller vi alla parametrar som behövs när du skapar en expertreplikation och varje körning skapas regelbundet.

För att indikera att en schemalagd experiment har skapats måste vi lägga till en `template` i själva förfrågningen. I `template`innehåller alla nödvändiga parametrar för schemaläggning av körningar, till exempel `tasks`, som anger vilken åtgärd som ska utföras, och `schedule`, som anger tidpunkten för de schemalagda körningarna.

**Begäran**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Datauppsättning som ska bokföras. Exemplet vi använder i vår självstudiekurs visas här:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

När vi skapar en expert, kroppen, `{JSON_PAYLOAD}`, ska innehålla antingen `mlInstanceId` eller `mlInstanceQuery` parameter. I det här exemplet anropar en schemalagd experiment en körning var 20:e minut som anges i `cron` parameter, från `startTime` tills `endTime`.

**Svar**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`: Det ID som representerar Experimenten.\
`{INSTANCE_ID}`: Det ID som representerar MLInstance.


### Skapa en provrunda för utbildning

När en experimentenhet har skapats kan en övning skapas och köras med hjälp av samtalet nedan. Du behöver `{EXPERIMENT_ID}` och ange vad `mode` som du vill utlösa i begärandetexten.

**Begäran**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`: Det ID som motsvarar den experiment som du vill använda som mål. Det här finns i svaret när du skapar din Experiment.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: För att kunna genomföra en utbildning måste du inkludera följande i brödtexten:

```JSON
{
    "mode":"Train"
}
```

Du kan även åsidosätta konfigurationsparametrarna genom att ta med en `tasks` array:

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

Du kommer att få följande svar som talar om för dig `{EXPERIMENT_RUN_ID}` och konfigurationen under `tasks`.

**Svar**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: Det ID som representerar Experimentkörningen.\
`{EXPERIMENT_ID}`: Det ID som representerar den experimentversion som Experiment Run är under.

### Hämta status för en experimentell körning

Status för Experimentkörningen kan efterfrågas med `{EXPERIMENT_RUN_ID}`.

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`: Det ID som representerar Experimenten.\
`{EXPERIMENT_RUN_ID}`: Det ID som representerar Experimentkörningen.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.

**Svar**

GET-samtalet ger status i `state` enligt nedan:

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`: Det ID som representerar Experimentkörningen.\
`{EXPERIMENT_ID}`: Det ID som representerar den experimentversion som Experiment Run är under.

Förutom `DONE` delstat, andra lägen:
- `PENDING`
- `RUNNING`
- `FAILED`

Detaljerade loggar finns under `tasklogs` parameter.

### Hämta den tränade modellen

För att få den tränade modell som skapats ovan under kursen ställer vi följande krav:

**Begäran**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar den Experimentkörning som du vill använda som mål. Detta finns i svaret när du skapar en Experiment Run.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.

Svaret representerar den tränade modell som skapades.

**Svar**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`: Det ID som motsvarar modellen.\
`{EXPERIMENT_ID}`: Det ID som motsvarar den Experiment som Experiment Run finns under.\
`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar Experimentkörningen.

### Stoppa och ta bort en schemalagd experiment

Om du vill avbryta körningen av en schemalagd expert innan den körs `endTime`kan du göra detta genom att fråga DELETE till `{EXPERIMENT_ID}`

**Begäran**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: Det ID som motsvarar Experimenten.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.

>[!NOTE]
>
>API-anropet inaktiverar skapandet av nya Experiment-körningar. Körningen av Experiment Runs avbryts dock inte.

Här följer ett svar som meddelar att experten har tagits bort.

**Svar**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## Nästa steg

Den här självstudiekursen gick igenom hur du använder API:erna för att skapa en motor, en experimentell, schemalagda Experimentrunda och tränade modeller. I [nästa övning](./score-model-api.md)kommer du att göra prognoser genom att betygsätta en ny datamängd med hjälp av den mest högpresterande tränade modellen.
