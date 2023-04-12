---
keywords: Experience Platform;Visa en modell;Datavetenskapen;populära ämnen;ensei machine learning api
solution: Experience Platform
title: Posta en modell med API:t för Sensei Machine Learning
type: Tutorial
description: I den här självstudiekursen får du lära dig hur du använder Sensei Machine Learning-API:erna för att skapa en Experiment och en Experimentrunda.
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Posta en modell med [!DNL Sensei Machine Learning API]

I den här självstudiekursen visas hur du använder API:erna för att skapa en Experiment och en ExperimentKör. En lista över alla slutpunkter i Sensei Machine Learning API finns på [det här dokumentet](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Skapa en schemalagd expert för poängsättning

På samma sätt som schemalagda utbildningsexperter, kan man även skapa en schemalagd utvärdering av poängsättningen genom att inkludera en `template` -avsnittet till body-parametern. Dessutom finns `name` fält under `tasks` i brödtexten är inställd som `score`.

Följande är ett exempel på hur du skapar en Experiment som körs var 20:e minut från `startTime` och kommer att köras tills `endTime`.

**Begäran**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{JSON_PAYLOAD}`: Objekt för experimentkörning som ska skickas. Exemplet vi använder i vår självstudiekurs visas här:

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`: Det ID som representerar MLInstance.\
`{MODEL_ID}`: Det ID som representerar den tränade modellen.

Följande är svaret efter att den schemalagda experten har skapats.

**Svar**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`: Det ID som representerar Experimenten.\
`{INSTANCE_ID}`: Det ID som representerar MLInstance.


### Skapa en provkörning för poängsättning

Med den tränade modellen kan vi nu skapa en Experiment Run för poängsättning. Värdet för `modelId` parametern är `id` parameter som returneras i GET Model-begäran ovan.

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

`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.\
`{EXPERIMENT_ID}`: Det ID som motsvarar den experiment som du vill använda som mål. Det här finns i svaret när du skapar din Experiment.\
`{JSON_PAYLOAD}`: Data som ska bokföras. Exemplet vi använder i vår självstudiekurs är här:

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`: Det ID som motsvarar modellen.

Svaret från att skapa en Experiment Run visas nedan:

**Svar**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: Det ID som motsvarar det Experiment som Kör finns under.\
`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar den Experimentkörning du just skapade.


### Hämta en status för experimentell körning för schemalagd experimentell körning

Om du vill hämta Experiment Runs för schemalagda experiment visas frågan nedan:

**Begäran**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`: Det ID som motsvarar det Experiment som Kör finns under.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{ORG_ID}`: Dina organisationsuppgifter finns i din unika Adobe Experience Platform-integration.

Eftersom det finns flera Experiment Runs för en viss Experiment har det returnerade svaret en array med Run ID:n.

**Svar**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar Experimentkörningen.\
`{EXPERIMENT_ID}`: Det ID som motsvarar det Experiment som Kör finns under.

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
