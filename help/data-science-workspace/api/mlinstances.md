---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära topics;mlinstances;sensei machine learning api
solution: Experience Platform
title: API-slutpunkt för MLInstances
topic: Developer guide
description: En MLInstance är en kombination av en befintlig motor med en lämplig uppsättning konfigurationer som definierar alla utbildningsparametrar, poängsättningsparametrar eller maskinvaruresurskonfigurationer.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# MLInstances-slutpunkt

En MLInstance är en kombination av en befintlig [motor](./engines.md) med en lämplig uppsättning konfigurationer som definierar alla utbildningsparametrar, poängsättningsparametrar eller maskinvaruresurskonfigurationer.

## Skapa en MLInstance {#create-an-mlinstance}

Du kan skapa en MLInstance genom att utföra en begäran om POST samtidigt som du anger en nyttolast som består av ett giltigt motor-ID (`{ENGINE_ID}`) och en lämplig uppsättning standardkonfigurationer.

Om motor-ID:t refererar till en PySpark- eller Spark-motor kan du konfigurera mängden beräkningsresurser, till exempel antalet kärnor eller mängden minne. Om du refererar till en Python Engine kan du välja mellan att använda en CPU eller GPU för utbildning och poängsättning. Mer information finns i avsnitten i bilagan om [PySpark- och Spark-resurskonfigurationer](./appendix.md#resource-config) och [Python CPU- och GPU-konfigurationer](./appendix.md#cpu-gpu-config).

**API-format**

```http
POST /mlInstances
```

**Begäran**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på MLInstance-instansen som du vill använda. Modellen som motsvarar denna MLInstance ärver det här värdet som ska visas i gränssnittet som modellens namn. |
| `description` | En valfri beskrivning för MLInstance. Modellen som motsvarar den här MLInstance ärver det här värdet som ska visas i gränssnittet som modellbeskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `engineId` | ID för en befintlig motor. |
| `tasks` | En uppsättning konfigurationer för utbildnings-, poängsättnings- eller funktionsledningar. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nyligen skapade MLInstance-instansen inklusive dess unika identifierare (`id`).

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Hämta en lista med MLInstances

Du kan hämta en lista med MLInstances genom att utföra en enda begäran om GET. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista över tillgängliga frågor finns i avsnittet i bilagan [frågeparametrar för hämtning](./appendix.md#query).

**API-format**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETER}` | En av de [tillgängliga frågeparametrarna](./appendix.md#query) som används för att filtrera resultat. |
| `{VALUE}` | Värdet för föregående frågeparameter. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med MLInstances och deras information.

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## Hämta en specifik MLInstance {#retrieve-specific}

Du kan hämta information om en viss MLInstance genom att utföra en GET-begäran som innehåller ID:t för den önskade MLInstance-instansen i sökvägen för begäran.

**API-format**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLINSTANCE_ID}` | ID för önskad MLInstance. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om MLInstance.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## Uppdatera en MLInstance

Du kan uppdatera en befintlig MLInstance genom att skriva över dess egenskaper via en PUT-begäran som innehåller mål-MLInstance-ID:t i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!TIP]
>
>För att försäkra dig om att denna PUT-begäran lyckas föreslår vi att du först utför en GET-begäran för att [hämta MLInstance med ID](#retrieve-specific). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

Följande exempel på API-anrop uppdaterar en MLInstance-instans utbildnings- och poängparametrar samtidigt som dessa egenskaper initialt finns:

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API-format**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLINSTANCE_ID}` | Ett giltigt MLInstance-ID. |

**Begäran**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den uppdaterade informationen för MLInstance-instansen.

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## Ta bort MLInstances efter motor-ID

Du kan ta bort alla MLInstances som delar samma motor genom att utföra en DELETE-begäran som innehåller motor-ID som frågeparameter.

**API-format**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | Ett giltigt motor-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "MLInstances successfully deleted"
}
```

## Ta bort en MLInstance

Du kan ta bort en enskild MLInstance genom att utföra en DELETE-begäran som innehåller målets MLInstance-ID i sökvägen för begäran.

**API-format**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MLINSTANCE_ID}` | Ett giltigt MLInstance-ID. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLInstance deletion was successful"
}
```
