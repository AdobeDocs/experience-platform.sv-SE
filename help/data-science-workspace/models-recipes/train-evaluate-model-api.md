---
keywords: Experience Platform;utbilda och utvärdera;Data Science Workspace;populära ämnen;Sensei Machine Learning API
solution: Experience Platform
title: Utbildning och utvärdering av en modell med Sensei Machine Learning API
type: Tutorial
description: I den här självstudiekursen visas hur du skapar, utbilda och utvärderar en modell med API-anrop för Sensei Machine Learning.
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# Utbilda och utvärdera en modell med API:t [!DNL Sensei Machine Learning]

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I den här självstudiekursen visas hur du skapar, utbilda och utvärderar en modell med API-anrop. Se [det här dokumentet](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) för en detaljerad lista över API-dokumentation.

## Förhandskrav

Följ [Importera ett paketerat recept med API:t ](./import-packaged-recipe-api.md) för att skapa en motor, vilket krävs för att träna och utvärdera en modell med API:t.

Följ självstudiekursen [Experience Platform API-autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att börja göra API-anrop.

Från självstudiekursen bör du nu ha följande värden:

- `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.
- `{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.
- `{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.

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

Du kan skapa en MLInstance med följande begäran. Du kommer att använda `{ENGINE_ID}` som returnerades när du skapade en motor från [Importera ett paketerat recept med hjälp av API](./import-packaged-recipe-ui.md)-självstudiekursen.

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

`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Konfigurationen av vår MLInstance. Exemplet som vi använder i vår självstudiekurs visas här:

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
>I `{JSON_PAYLOAD}` definierar vi parametrar som används för utbildning och poängsättning i arrayen `tasks`. `{ENGINE_ID}` är ID:t för den motor som du vill använda och fältet `tag` är en valfri parameter som används för att identifiera instansen.

Svaret innehåller `{INSTANCE_ID}` som representerar den MLInstance som skapas. Flera MLInstances-modeller med olika konfigurationer kan skapas.

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

En datavetare använder en expert för att komma fram till en högpresterande modell under utbildningen. Det finns många olika experimentalternativ, till exempel föränderliga datauppsättningar, funktioner, inlärningsparametrar och maskinvara. Följande är ett exempel på hur du skapar en expert.

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

`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Experimentera objekt som skapas. Exemplet som vi använder i vår självstudiekurs visas här:

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

Om du vill ange att en schemalagd utvärderingsprocess ska skapas måste vi lägga till ett `template`-avsnitt i förfrågningens innehåll. I `template` inkluderas alla nödvändiga parametrar för schemaläggning av körningar, till exempel `tasks`, som anger vilken åtgärd och `schedule` som anger tidpunkten för schemalagda körningar.

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

`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Datauppsättning som ska bokföras. Exemplet som vi använder i vår självstudiekurs visas här:

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

När vi skapar en expert ska brödtexten, `{JSON_PAYLOAD}`, innehålla antingen parametern `mlInstanceId` eller `mlInstanceQuery`. I det här exemplet kommer en schemalagd experiment att anropa en körning var 20:e minut som anges i parametern `cron`, med början från `startTime` till `endTime`.

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

När en experimentenhet har skapats kan en övning skapas och köras med hjälp av samtalet nedan. Du behöver `{EXPERIMENT_ID}` och anger vad `mode` du vill utlösa i begärandetexten.

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
`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Om du vill skapa en utbildningskurs måste du inkludera följande i brödtexten:

```JSON
{
    "mode":"Train"
}
```

Du kan även åsidosätta konfigurationsparametrarna genom att ta med en `tasks`-matris:

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

Du får följande svar som meddelar dig om `{EXPERIMENT_RUN_ID}` och konfigurationen under `tasks`.

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
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.

**Svar**

GET-anropet ger status i parametern `state` enligt nedan:

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

Förutom läget `DONE` innehåller andra lägen:
- `PENDING`
- `RUNNING`
- `FAILED`

Mer information finns i detaljerade loggar under parametern `tasklogs`.

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
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.

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
`{EXPERIMENT_ID}`: Det ID som motsvarar det experiment som Experiment Run körs under.\
`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar Experiment Run.

### Stoppa och ta bort en schemalagd experiment

Om du vill avbryta körningen av en schemalagd experiment innan `endTime` körs kan du göra det genom att fråga en DELETE-begäran till `{EXPERIMENT_ID}`

**Begäran**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: ID:t som motsvarar Experiment.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.\
`{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.

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

Den här självstudiekursen gick igenom hur du använder API:erna för att skapa en motor, en experimentell, schemalagda Experimentrunda och tränade modeller. I [nästa övning](./score-model-api.md) kommer du att göra prognoser genom att göra en bedömning av en ny datauppsättning med hjälp av den bäst fungerande, tränade modellen.
