---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Insikter
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Insikter

Insikter innehåller mätvärden som används för att ge datavetare möjlighet att utvärdera och välja optimala ML-modeller genom att visa relevanta utvärderingsvärden.

## Hämta en lista med insikter

Du kan hämta en lista med insikter genom att utföra en GET-begäran till insikter-slutpunkten.  Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

**API-format**

```http
GET /insights
```

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller en lista med insikter och varje insikt har en unik identifierare ( `id` ). Dessutom får ni `context` som innehåller de unika identifierare som är kopplade till den specifika insikten som följer med Insights-händelser och mätdata.

```json
{
    "children": [
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "{INSIGHT_ID}",
            "context": {
                "experimentId": "{EXPERIMENT_ID}",
                "experimentRunId": "{EXPERIMENT_RUN_ID}",
                "modelId": "{MODEL_ID}"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar Insight. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |
| `modelId` | Ett giltigt modell-ID. |

## Hämta en specifik insight

Om du vill söka efter en viss insikt kan du göra en GET-begäran och ange en giltig `{INSIGHT_ID}` i sökvägen för begäran. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

**API-format**

```http
GET /insights/{INSIGHT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{INSIGHT_ID}` | Den unika identifieraren för en Sensei-insikt. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/{INSIGHT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den unika identifieraren (`id`) för insikter. Dessutom får ni `context` som innehåller de unika identifierare som är kopplade till den särskilda insikt som följer med Insights-händelser och mätdata.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Det ID som motsvarar Insight. |
| `experimentId` | Ett giltigt test-ID. |
| `experimentRunId` | Ett giltigt ID för Experiment Run. |
| `modelId` | Ett giltigt modell-ID. |

## Lägg till en ny modellinsikt

Du kan skapa en ny modellinsikt genom att utföra en POST-begäran och en nyttolast som ger kontext, händelser och mått för den nya modellinsikten. Det kontextfält som används för att skapa en ny modellinsikt behöver inte ha befintliga tjänster kopplade till sig, men du kan välja att skapa den nya modellinsikten med befintliga tjänster genom att tillhandahålla ett eller flera motsvarande ID:

```json
"context": {
    "clientId": "{CLIENT_ID}",
    "notebookId": "{NOTEBOOK_ID}",
    "experimentId": "{EXPERIMENT_ID}",
    "engineId": "{ENGINE_ID}",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "modelId": "{MODEL_ID}",
    "dataSetId": "{DATASET_ID}"
  }
```

**API-format**

```http
POST /insights
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**Svar**

Ett lyckat svar returnerar en nyttolast som har en `{INSIGHT_ID}` och alla parametrar som du angav i den ursprungliga begäran.

```json
{
    "id": "{INSIGHT_ID}",
    "context": {
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "modelId": "{MODEL_ID}"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `insightId` | Det unika ID som skapas för den här informationen när en POST-begäran görs. |

## Hämta en lista med standardvärden för algoritmer

Du kan hämta en lista över alla algoritmernas och standardmåtten genom att utföra en GET-begäran till metrisk slutpunkt. Om du vill fråga efter ett visst mått skapar du en GET-begäran och anger en giltig `{ALGORITHM}` i sökvägen till begäran.

**API-format**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ALGORITHM}` | Identifieraren för algoritmtypen. |

**Begäran**

Följande begäran innehåller en fråga och hämtar ett specifikt mått med algoritmidentifieraren `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller den `algorithm` unika identifieraren och en matris med standardmått.

```json
{
    "children": [
        {
            "algorithm": "{ALGORITHM}",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```
