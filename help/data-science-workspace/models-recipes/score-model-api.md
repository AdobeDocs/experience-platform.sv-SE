---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Posta en modell (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Posta en modell (API)

I den här självstudiekursen visas hur du använder API:erna för att skapa en Experiment och en ExperimentKör. En detaljerad lista över API-dokumentation finns i [det här dokumentet](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html).

## Skapa en schemalagd expert för poängsättning

På samma sätt som schemalagda övningar för utbildning, görs också en schemalagd utvärdering av poängsättningen genom att en del av `template` body-parametern tas med. Dessutom ställs fältet under `name``tasks` i brödtexten in som `score`.

Följande är ett exempel på hur du skapar en Experiment som körs var 20:e minut från `startTime` och kommer att köras tills `endTime`.

**Begäran**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Dina IMS-organisationsuppgifter hittades i din unika integrering med Adobe Experience Platform.\
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

Med den tränade modellen kan vi nu skapa en Experiment Run för poängsättning. Värdet på `modelId` parametern är den `id` parameter som returneras i GET Model-begäran ovan.

**Begäran**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`: Dina IMS-organisationsuppgifter hittades i din unika integrering med Adobe Experience Platform.\
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

`{EXPERIMENT_ID}`:  Det ID som motsvarar det Experiment som Kör finns under.\
`{EXPERIMENT_RUN_ID}`: Det ID som motsvarar den Experimentkörning du just skapade.


### Hämta en status för experimentell körning för schemalagd experimentell körning

Om du vill hämta Experiment Runs för schemalagda experiment visas frågan nedan:

**Begäran**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  Det ID som motsvarar det Experiment som Kör finns under.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{IMS_ORG}`: Dina IMS-organisationsuppgifter hittades i din unika integrering med Adobe Experience Platform.

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
`{EXPERIMENT_ID}`:  Det ID som motsvarar det Experiment som Kör finns under.

### Stoppa och ta bort en schemalagd experiment

Om du vill avbryta körningen av en schemalagd experiment innan den körs `endTime`kan du göra det genom att fråga en DELETE-begäran till `{EXPERIMENT_ID}`

**Begäran**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:  ID:t som motsvarar Experiment.\
`{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.\
`{IMS_ORG}`: Dina IMS-organisationsuppgifter hittades i din unika integrering med Adobe Experience Platform.

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
