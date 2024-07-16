---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära ämnen;insights;sensei machine learning api
solution: Experience Platform
title: API-slutpunkt för insikter
description: Insikter innehåller mätvärden som används för att ge datavetare möjlighet att utvärdera och välja optimala ML-modeller genom att visa relevanta utvärderingsvärden.
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Insikter, slutpunkt

Insikter innehåller mätvärden som används för att ge datavetare möjlighet att utvärdera och välja optimala ML-modeller genom att visa relevanta utvärderingsvärden.

## Hämta en lista med insikter

Du kan hämta en lista med insikter genom att utföra en enda GET-förfrågan till insikter-slutpunkten.  Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om tillägg för [frågeparametrar för hämtning av resurser](./appendix.md#query).

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller en lista med insikter och varje insikter har en unik identifierare ( `id` ). Dessutom får du `context` som innehåller de unika identifierare som är associerade med den specifika insikten som följer med Insights-händelser och mätdata.

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Om du vill söka efter en viss insikt kan du göra en GET-förfrågan och ange en giltig `{INSIGHT_ID}` i sökvägen för begäran. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om tillägg för [frågeparametrar för hämtning av resurser](./appendix.md#query).

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
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den unika identifieraren (`id`) för insikter. Dessutom kommer du att få `context` som innehåller de unika identifierare som är associerade med den särskilda insikten som följer med Insights-händelser och mätdata.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Du kan skapa en ny modellinsikt genom att utföra en modellförfrågan och en nyttolast som ger kontext, händelser och mätvärden för den nya modellinsikten. Det kontextfält som används för att skapa en ny modellinsikt behöver inte ha befintliga tjänster kopplade till sig, men du kan välja att skapa den nya modellinsikten med befintliga tjänster genom att tillhandahålla ett eller flera motsvarande ID:

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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

Ett lyckat svar returnerar en nyttolast som har `{INSIGHT_ID}` och alla parametrar som du har angett i den ursprungliga begäran.

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
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
| `insightId` | Det unika ID som skapas för den här informationen när en begäran om POST har gjorts. |

## Hämta en lista med standardvärden för algoritmer

Du kan hämta en lista över alla algoritmernas och standardmåtten genom att utföra en enda GET-begäran till metrisk slutpunkt. Om du vill fråga efter ett visst mått gör du en GET-förfrågan och anger en giltig `{ALGORITHM}` i sökvägen för begäran.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den unika identifieraren `algorithm` och en matris med standardmått.

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
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
