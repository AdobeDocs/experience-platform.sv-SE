---
keywords: Experience Platform;publicera en modell;Data Science Workspace;populära ämnen;sensei machine learning api
solution: Experience Platform
title: Publish a Model as a Service Using the Sensei Machine Learning API
type: Tutorial
description: I den här självstudiekursen beskrivs hur du publicerar en modell som en tjänst med Sensei Machine Learning API.
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 0%

---

# Publish en modell som en tjänst med [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I den här självstudien beskrivs processen att publicera en modell som en tjänst med hjälp av [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för Adobe Experience Platform Data Science Workspace. Innan du börjar med den här självstudiekursen bör du gå igenom [Workspace-översikten för datavetenskap](../home.md) för att få en introduktion till tjänsten på hög nivå.

Om du vill följa med i den här självstudiekursen måste du ha en befintlig ML-motor, ML-instans och Experiment. Anvisningar om hur du skapar dessa i API:t finns i självstudiekursen [Importera ett paketerat recept](./import-packaged-recipe-api.md).

Innan du startar den här självstudiekursen bör du gå igenom avsnittet [Komma igång](../api/getting-started.md) i utvecklarhandboken för att få viktig information som du behöver känna till för att kunna anropa API:t för [!DNL Sensei Machine Learning], inklusive de rubriker som krävs som används i den här självstudiekursen:

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

Alla förfrågningar från POST, PUT och PATCH kräver ytterligare en rubrik:

- Content-Type: application/json

### Nyckeltermer

I följande tabell beskrivs några vanliga termer som används i den här självstudiekursen:

| Villkor | Definition |
| --- | --- |
| **Instans för maskininlärning (ML-instans)** | En instans av en [!DNL Sensei]-motor för en viss klientorganisation som innehåller specifika data, parametrar och [!DNL Sensei]-kod. |
| **Experimentera** | En paraplyenhet för utbildning Experiment Runs, Scoring Experiment Runs, eller båda. |
| **Schemalagd experiment** | En term som beskriver automatiseringen av kurser eller poängsättning i Experiment Runs som styrs av ett användardefinierat schema. |
| **Experimentkörning** | Ett särskilt fall av utbildning eller poängsättningsexperiment. Multipla Experiment körs från en viss Experiment och kan skilja sig åt när det gäller datamängder som används för utbildning eller poängsättning. |
| **Utbildad modell** | En maskininlärningsmodell som har skapats genom att experimentera och använda konstruktion innan den levereras till en validerad, utvärderad och färdigställd modell. |
| **Publicerad modell** | En färdig och versionshanterad modell som tagits fram efter utbildning, validering och utvärdering. |
| **Maskinininlärningstjänst (ML-tjänst)** | En ML-instans distribuerad som en tjänst för att stödja on-demand-begäranden om utbildning och poängsättning med en API-slutpunkt. En ML-tjänst kan också skapas med befintliga utbildade Experiment Runs. |

## Skapa en ML-tjänst med en befintlig övningsexperimentell körning och schemalagd poängsättning

När du publicerar en utbildningsexperimentell körning som en ML-tjänst kan du schemalägga betygsättning genom att ange information för bedömningsförsöket Kör nyttolasten för en POST. Detta resulterar i att en schemalagd experimententitet för poängsättning skapas.

**API-format**

```http
POST /mlServices
```

**Begäran**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `mlInstanceId` | Befintlig ML-instans-identifiering, ska den träningsutvärderingsrunda som används för att skapa ML-tjänsten motsvara den här speciella ML-instansen. |
| `trainingExperimentId` | Experimentera-ID som motsvarar ML-instansidentifieringen. |
| `trainingExperimentRunId` | En särskild utbildning Experiment Run som ska användas för att publicera ML-tjänsten. |
| `scoringDataSetId` | Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök. |
| `scoringTimeframe` | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `10080` innebär till exempel att data från de senaste 10080 minuterna eller 168 timmar kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att värdet `0` inte kommer att filtrera data. Alla data i datauppsättningen används för poängsättningen. |
| `scoringSchedule` | Innehåller information om schemalagda poängsättningsförsök. |
| `scoringSchedule.startTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.endTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.cron` | Kroniskt värde som anger intervallet för när Experiment Runs ska poängsättas. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade ML-tjänsten, inklusive dess unika `id` och `scoringExperimentId` för motsvarande poängsättningsexperiment.


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## Skapa en ML-tjänst från en befintlig ML-instans

Beroende på ditt specifika användningsfall och dina specifika krav är det flexibelt att skapa en ML-tjänst med en ML-instans när det gäller schemaläggning av kurser och poängsättning i Experiment Runs. Den här självstudiekursen handlar om följande specialfall:

- [Du behöver ingen schemalagd utbildning, men du måste göra en schemalagd poängsättning.](#ml-service-with-scheduled-experiment-for-scoring)
- [Du behöver schemalagda utvärderingsversioner för både utbildning och poängsättning.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observera att en ML-tjänst kan skapas med en ML-instans utan schemaläggning av några utbildnings- eller poängsättningsexperiment. Sådana ML-tjänster kommer att skapa vanliga experimentenheter och en enda Experimentrunda för utbildning och poängsättning.

### ML-tjänst med schemalagd utvärdering för bedömning {#ml-service-with-scheduled-experiment-for-scoring}

Du kan skapa en ML-tjänst genom att publicera en ML-instans med schemalagda Experiment Runs för bedömning, som skapar en vanlig Experimentenhet för utbildning. En utbildnings-Experimentkörning genereras och kommer att användas för alla schemalagda poängsättningsutvärderingsutvärderingsprocesser. Kontrollera att du har `mlInstanceId`, `trainingDataSetId` och `scoringDataSetId` som krävs för att skapa ML-tjänsten och att de finns och är giltiga värden.

**API-format**

```http
POST /mlServices
```

**Begäran**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-tangent | Beskrivning |
| --- | --- |
| `mlInstanceId` | Befintlig ML-instans-ID, som representerar ML-instansen som används för att skapa ML-tjänsten. |
| `trainingDataSetId` | Identifiering som avser den specifika datauppsättning som ska användas för utbildningsexperiment. |
| `trainingTimeframe` | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för utbildning av Experiment. Värdet `"10080"` innebär till exempel att data från de senaste 10080 minuterna eller 168 timmar kommer att användas för att utbilda Experiment Run. Observera att värdet `"0"` inte filtrerar data. Alla data i datauppsättningen används för utbildning. |
| `scoringDataSetId` | Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök. |
| `scoringTimeframe` | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `"10080"` innebär till exempel att data från de senaste 10080 minuterna eller 168 timmar kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att värdet `"0"` inte kommer att filtrera data. Alla data i datauppsättningen används för poängsättningen. |
| `scoringSchedule` | Innehåller information om schemalagda poängsättningsförsök. |
| `scoringSchedule.startTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.endTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.cron` | Kroniskt värde som anger intervallet för när Experiment Runs ska poängsättas. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade ML-tjänsten. Detta inkluderar tjänstens unika `id` samt `trainingExperimentId` och `scoringExperimentId` för motsvarande utbildning och poängsättningsexperiment.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### ML-tjänst med schemalagda experiment för utbildning och poängsättning {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Om du vill publicera en befintlig ML-instans som en ML-tjänst med schemalagda kurser och poängsättningsprovperioder måste du tillhandahålla både utbildnings- och poängscheman. När en ML-tjänst av den här konfigurationen skapas skapas även schemalagda experimentenheter för både utbildning och poängsättning. Observera att kursplaner och poängscheman inte behöver vara desamma. Under ett poängsättningsjobb kommer den senaste utbildningsmodellen som skapats av schemalagda kurser i Experiment Runs att hämtas och användas för den schemalagda poängsättningen.

**API-format**

```http
POST /mlServices
```

**Begäran**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON-tangent | Beskrivning |
| --- | --- |
| `mlInstanceId` | Befintlig ML-instans-ID, som representerar ML-instansen som används för att skapa ML-tjänsten. |
| `trainingDataSetId` | Identifiering som avser den specifika datauppsättning som ska användas för utbildningsexperiment. |
| `trainingTimeframe` | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för utbildning av Experiment. Värdet `"10080"` innebär till exempel att data från de senaste 10080 minuterna eller 168 timmar kommer att användas för att utbilda Experiment Run. Observera att värdet `"0"` inte filtrerar data. Alla data i datauppsättningen används för utbildning. |
| `scoringDataSetId` | Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök. |
| `scoringTimeframe` | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `"10080"` innebär till exempel att data från de senaste 10080 minuterna eller 168 timmar kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att värdet `"0"` inte kommer att filtrera data. Alla data i datauppsättningen används för poängsättningen. |
| `trainingSchedule` | Innehåller information om schemalagda kurser i Experimentprogram. |
| `scoringSchedule` | Innehåller information om schemalagda poängsättningsförsök. |
| `scoringSchedule.startTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.endTime` | Datum och tid som anger när poängsättningen ska börja. |
| `scoringSchedule.cron` | Kroniskt värde som anger intervallet för när Experiment Runs ska poängsättas. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade ML-tjänsten. Detta inkluderar tjänstens unika `id`, samt `trainingExperimentId` och `scoringExperimentId` för motsvarande utbildnings- och poängsättningsexperiment. I exempelsvaret nedan tyder närvaron av `trainingSchedule` och `scoringSchedule` på att Experimententiteterna för utbildning och poängsättning är schemalagda experiment.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## Söka efter en ML-tjänst {#retrieving-ml-services}

Du kan söka efter en befintlig ML-tjänst genom att göra en `GET`-begäran till `/mlServices` och ange den unika `id` för ML-tjänsten i sökvägen.

**API-format**

```http
GET /mlServices/{SERVICE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SERVICE_ID}` | Den unika `id` för ML-tjänsten som du söker efter. |

**Begäran**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar information om ML-tjänsten.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>Hämtning av olika ML-tjänster kan returnera ett svar med fler eller färre nyckelvärdepar. Ovanstående svar är en representation av en [ML-tjänst med både schemalagda utbildnings- och poängsättningsutvärderingsversioner](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Schemalägg utbildning eller poängsättning

Om du vill schemalägga poängsättning och utbildning för en ML-tjänst som redan har publicerats kan du göra det genom att uppdatera den befintliga ML-tjänsten med en `PUT`-begäran `/mlServices`.

**API-format**

```http
PUT /mlServices/{SERVICE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SERVICE_ID}` | Den unika `id` för ML-tjänsten som du uppdaterar. |

**Begäran**

Följande begäran schemalägger utbildning och poängsättning för en befintlig ML-tjänst genom att lägga till nycklarna `trainingSchedule` och `scoringSchedule` med respektive tangent `startTime`, `endTime` och `cron`.

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>Försök inte ändra `startTime` för befintliga schemalagda utbildnings- och poängsättningsjobb. Om `startTime` måste ändras bör du överväga att publicera samma modell och schemalägga om utbildnings- och bedömningsjobb.

**Svar**

Ett godkänt svar returnerar information om den uppdaterade ML-tjänsten.

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```
