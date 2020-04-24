---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicera en modell som en tjänst (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Publicera en modell som en tjänst (API)

## Förutsättningar

- Följ den här [självstudiekursen](../../tutorials/authentication.md) för att börja göra API-anrop.
Från självstudiekursen bör du nu ha följande information:
   - `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
   - `{IMS_ORG}`: Dina IMS-organisationsuppgifter finns i din unika integrering med Adobe Experience Platform.
   - `{API_KEY}`: Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- Den här självstudiekursen kräver befintliga ML-motorer, ML-instanser och experimententiteter. Se den här [självstudiekursen](./import-packaged-recipe-api.md) om hur du skapar ML-motor, ML-instans eller Experimententiteter.
- Mer information om API-slutpunkter och förfrågningar som omnämns i den här självstudiekursen finns i det fullständiga API:t för [Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## Nyckeltermer

En del vanliga termer som används i den här självstudiekursen:

| Term | Definition |
--- | ---
| **Machine Learning-instans (ML-instans)** | Den konceptuella entiteten som är en instans av en Sensei Engine för en viss klientorganisation som består av specifika data, parametrar och Sensei-kod. |
| **Experimentera** | En paraplyenhet för utbildning Experiment Runs, Scoring Experiment Runs eller båda. |
| **Schemalagd experiment** | En term som beskriver automatiseringen av kurser eller poängsättning i Experiment Runs som styrs av ett användardefinierat schema. |
| **Experimentera** | Ett särskilt fall av utbildning eller poängsättningsexperiment. Multipla Experiment körs från en viss Experiment och kan skilja sig åt i datauppsättningsvärden som används för utbildning eller poängsättning. |
| **Utbildad modell** | En maskininlärningsmodell som har skapats genom att experimentera och använda konstruktion innan den levereras till en validerad, utvärderad och färdigställd modell. |
| **Publicerad modell** | En färdig och versionshanterad modell som tagits fram efter utbildning, validering och utvärdering. |
| **Machine Learning-tjänst (ML-tjänst)** | En ML-instans distribuerad som en tjänst som stöder on demand-begäran om utbildning och poängsättning via en slutpunkt. Observera att en ML-tjänst också kan skapas med befintliga, utbildade experimentella körningar. |


## API-arbetsflöde

Den här självstudiekursen går vidare till att skapa, hämta och uppdatera en ML-tjänst.

## Skapa en ML-tjänst med en befintlig utbildning Experimentera Run och schemalagd poängsättning

När du publicerar en utbildningsexperimentell körning som en ML-tjänst kan du schemalägga betygsättning genom att ange information för betygsförsökskörningen i `scoringSchedule` din {JSON_PAYLOAD}. Detta resulterar i att en schemalagd experimententitet för poängsättning skapas. Kontrollera att du har `mlInstanceId`, `trainingExperimentId`, `trainingExperimentRunId`, `scoringDataSetId`och att de finns och är giltiga värden.

Börja med att göra en `POST` förfrågan till `/mlServices`. Nedan visas ett exempel på ett rullande kommando:

**Begäran**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- `{IMS_ORG}` :  Ditt IMS-organisations-ID finns under integreringsinformationen i Adobe I/O Console.
- `{ACCESS_TOKEN}` : Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{JSON_PAYLOAD}` : Ett exempel på JSON-nyttolastformat visas nedan:

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` : Befintlig ML-instans-identifiering, ska den träningsutvärderingsrunda som används för att skapa ML-tjänsten motsvara den här speciella ML-instansen.
- `trainingExperimentId` : Experimentera-ID som motsvarar ML-instansidentifieringen.
- `trainingExperimentRunId` : En särskild utbildning Experiment Run som ska användas för att publicera ML-tjänsten.
- `scoringDataSetId` : Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök.
- `scoringTimeframe` : Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `"10080"` betyder till exempel att data från de senaste 10080 minuterna eller 168 timmarna kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att ett värde på `"0"` inte filtrerar data, att alla data i datauppsättningen används för bedömning.
- `scoringSchedule` : Innehåller information om schemalagda poängsättningsförsök.
- `startTime` : definition.
- `endTime` : definition.
- `cron` : definition.

**Svar**

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

Från JSON-svaret visar nyckeln `scoringExperimentId` med dess motsvarande värde att en ny bedömningsexpert skapades tillsammans med det experimentschema som du angav i `POST` begäran. Nyckeln i svaret identifierar `id` den XML-tjänst som skapades.

## Skapa en ML-tjänst från en befintlig ML-instans

Beroende på ditt specifika användningsfall och dina specifika krav är det flexibelt att skapa en ML-tjänst med en ML-instans när det gäller schemaläggning av kurser och poängsättning i Experiment Runs. Den här självstudiekursen handlar om följande specialfall:

- [Du behöver ingen schemalagd utbildning, men du måste göra en schemalagd poängsättning.](#ml-service-with-scheduled-experiment-for-scoring)
- [Du behöver schemalagda utvärderingsversioner för både utbildning och poängsättning.](#ml-service-with-scheduled-experiments-for-training-and-scoring)

Observera att en ML-tjänst kan skapas med en ML-instans utan schemaläggning av några utbildnings- eller poängsättningsexperiment. Sådan ML-tjänst skapar vanliga experimentenheter och en enda Experimentrunda för utbildning och poängsättning.

### ML-tjänst med schemalagd utvärdering för bedömning {#ml-service-with-scheduled-experiment-for-scoring}

Om du skapar en ML-tjänst genom att publicera en ML-instans med schemalagda utvärderingsprocesser för poängsättning skapas en vanlig experimententitet för utbildning. Den resulterande utbildnings-Experimentkörningen som genereras kommer att användas för alla schemalagda poängsättningsförsök. Kontrollera att du har de `mlInstanceId`, `trainingDataSetId`och `scoringDataSetId` obligatoriska data som behövs för att skapa ML-tjänsten och att de finns och är giltiga värden.

Börja med att göra en `POST` förfrågan till `/mlServices`. Nedan visas ett exempel på ett rullande kommando:

**Begäran**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` : Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- `{IMS_ORG}` :  Ditt IMS-organisations-ID finns under integreringsinformationen i Adobe I/O Console.
- `{ACCESS_TOKEN}` : Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{JSON_PAYLOAD}` : Ett exempel på JSON-nyttolastformat visas nedan:

```JSON
{
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
}
```

| JSON-tangent | Beskrivning |
| --- | --- |
| **`mlInstanceId`** | Befintlig ML-instans-ID, som representerar ML-instansen som används för att skapa ML-tjänsten. |
| **`trainingDataSetId`** | Identifiering som avser den specifika datauppsättning som ska användas för utbildningsexperiment. |
| **`trainingTimeframe`** | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för utbildning av Experiment. Värdet `"10080"` betyder till exempel att data från de senaste 10080 minuterna eller 168 timmarna kommer att användas för att utbilda Experiment Run. Observera att värdet `"0"` inte filtrerar data, att alla data i datauppsättningen används för utbildning. |
| **`scoringDataSetId`** | Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök. |
| **`scoringTimeframe`** | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `"10080"` betyder till exempel att data från de senaste 10080 minuterna eller 168 timmarna kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att ett värde på `"0"` inte filtrerar data, att alla data i datauppsättningen används för bedömning. |
| **`scoringSchedule`** | Innehåller information om schemalagda poängsättningsförsök. |

**Svar**

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

Från `JSON` svaret, tangenterna `trainingExperimentId` och `scoringExperimentId` antyder att en ny tränings- och poängsättningsexpert skapades för denna ML-tjänst. Objektets närvaro hänvisar till information om schemat för `scoringSchedule` bedömningsförsökskörning. Nyckeln i svaret refererar till den ML-tjänst du just har skapat. `id`

### ML-tjänst med schemalagda experiment för utbildning och poängsättning {#ml-service-with-scheduled-experiments-for-training-and-scoring}

Om du vill publicera en befintlig ML-instans som en ML-tjänst med schemalagda kurser och poängsättningsprovperioder måste du tillhandahålla både utbildnings- och poängscheman. När en ML-tjänst av den här konfigurationen skapas skapas även schemalagda experimentenheter för både utbildning och poängsättning. Observera att kursplaner och poängscheman inte behöver vara desamma. Under ett poängsättningsjobb kommer den senaste utbildningsmodellen som skapats av schemalagda kurser i Experiment Runs att hämtas och användas för den schemalagda poängsättningen.

Skapa ML-tjänsten genom att göra en `POST` begäran `/mlServices` med det `{JSON_PAYLOAD}` som representerar det ML-tjänstobjekt som ska läggas till. Kontrollera att `mlInstanceId`, `trainingDataSetId`och `scoringDataSetId` finns och är giltiga värden.

**Begäran**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` : Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- `{IMS_ORG}` :  Ditt IMS-organisations-ID finns under integreringsinformationen i Adobe I/O Console.
- `{ACCESS_TOKEN}` : Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{JSON_PAYLOAD}` : Ett exempel på JSON-nyttolastformat visas nedan:

```JSON
{
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
}
```

| JSON-tangent | Beskrivning |
| --- | --- |
| **`mlInstanceId`** | Befintlig ML-instans-ID, som representerar ML-instansen som används för att skapa ML-tjänsten. |
| **`trainingDataSetId`** | Identifiering som avser den specifika datauppsättning som ska användas för utbildningsexperiment. |
| **`trainingTimeframe`** | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för utbildning av Experiment. Värdet `"10080"` betyder till exempel att data från de senaste 10080 minuterna eller 168 timmarna kommer att användas för att utbilda Experiment Run. Observera att värdet `"0"` inte filtrerar data, att alla data i datauppsättningen används för utbildning. |
| **`scoringDataSetId`** | Identifiering som refererar till den specifika datauppsättning som ska användas för schemalagda poängsättningsförsök. |
| **`scoringTimeframe`** | Ett heltalsvärde som representerar minuter för filtrering av data som ska användas för poängsättning av Experiment Runs. Värdet `"10080"` betyder till exempel att data från de senaste 10080 minuterna eller 168 timmarna kommer att användas för varje schemalagd bedömningsutvärderingskörning. Observera att ett värde på `"0"` inte filtrerar data, att alla data i datauppsättningen används för bedömning. |
| **`trainingSchedule`** | Innehåller information om schemalagda kurser i Experimentprogram. |
| **`scoringSchedule`** | Innehåller information om schemalagda poängsättningsförsök. |

**Svar**

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

Tillägg av `trainingExperimentId` och `scoringExperimentId` i svarsorganet föreslår att expertenheter skapas för både utbildning och poängsättning. Förekomsten av `trainingSchedule` och `scoringSchedule` antyder att de ovannämnda expertenheterna för utbildning och poängsättning är inplanerade experiment. Nyckeln i svaret refererar till den ML-tjänst du just har skapat. `id`

## Hämtar ML-tjänster {#retrieving-ml-services}

Att hämta en befintlig ML-tjänst är så enkelt som att göra en `GET` begäran till `/mlServices` slutpunkten. Kontrollera att du har ML-tjänstidentifieringen för den specifika ML-tjänst du försöker hämta.

**Begäran**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` : Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- `{IMS_ORG}` :  Ditt IMS-organisations-ID finns under integreringsinformationen i Adobe I/O Console.
- `{ACCESS_TOKEN}` : Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.

**Svar**

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

JSON-svaret representerar ML-tjänstobjektet. Det här objektet motsvarar svaret för när ML-tjänsten skapas. Observera att hämtning av olika ML-tjänster kan returnera ett svar med fler eller färre nyckelvärdepar. Ovanstående svar är en representation av en [ML-tjänst med både schemalagda kurser och poängsättningsprovperioder](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## Schemalägg utbildning eller poängsättning

Anta att du vill schemalägga poängsättning och utbildning för en ML-tjänst som redan har publicerats, så kan du göra det genom att uppdatera den befintliga ML-tjänsten med en `PUT` begäran på `/mlServices`. Kontrollera att du har det ML-tjänstidentifieringsprogram som du vill uppdatera. Som referens kan det vara ett bra första steg att [hämta ML-tjänsten](#retrieving-ml-services) som du vill uppdatera.

**Begäran**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` : Unik identifiering som refererar till ML-tjänsten som du vill uppdatera.
- `{API_KEY}` : Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.
- `{IMS_ORG}` :  Ditt IMS-organisations-ID finns under integreringsinformationen i Adobe I/O Console.
- `{ACCESS_TOKEN}` : Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{JSON_PAYLOAD}` : Ett exempel på JSON-nyttolastformat visas nedan:

```JSON
{
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
}
```

Schemaläggning av utbildning och poängsättning kan göras genom att lägga till `trainingSchedule` och `scoringSchedule` med respektive `startTime`, `endTime`och `cron` .

>[!NOTE] som `PUT` aktiverats `mlServices` gör det möjligt att ändra tjänster med befintliga schemalagda experimentperioder. Försök **inte** att ändra `startTime` befintliga schemalagda utbildnings- och poängsättningsjobb. Om mallen `startTime` måste ändras bör du överväga att publicera samma modell och att omplanera kursen och poängsättningen.

**Svar**

Svaret blir `{JSON_PAYLOAD}` men med extra `id`, `created`och `updated` tangenter i objektet.

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
