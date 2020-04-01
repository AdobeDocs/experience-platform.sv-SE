---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Modeller
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Modeller

En modell är en instans av ett maskininlärningsrecept som är utbildat med historiska data och konfigurationer för att lösa ett affärsärende.

## Hämta en lista med modeller

Du kan hämta en lista med modellinformation som tillhör alla modeller genom att utföra en GET-begäran till /models. Som standard sorteras den här listan från den äldsta modellen och resultatet begränsas till 25. Du kan välja att filtrera resultaten genom att ange vissa frågeparametrar. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

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

Ett godkänt svar returnerar en nyttolast som innehåller information om modellerna inklusive varje Models unika identifierare (`id`).

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
| `modelArtifactUri` | En URI som anger var modellen lagras. URI:n avslutas med modellens `name` värde. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |

## Hämta en specifik modell

Du kan hämta en lista med modellinformation som tillhör en viss modell genom att utföra en GET-begäran och ange ett giltigt modell-ID i sökvägen för begäran. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

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
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om din modell inklusive den unika identifieraren (`id`) för modellerna.

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar modellen. |
| `modelArtifactUri` | En URI som anger var modellen lagras. URI:n avslutas med modellens `name` värde. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |

## Uppdatera en modell med ID

Du kan uppdatera en befintlig modell genom att skriva över dess egenskaper via en PUT-begäran som inkluderar målmodellens ID i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP] För att säkerställa att denna PUT-begäran lyckas föreslår vi att du först utför en GET-begäran för att hämta modellen efter ID. Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
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
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
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
