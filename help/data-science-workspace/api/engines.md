---
keywords: Experience Platform;utvecklarguide;endpoint;Data Science Workspace;populära topics;engines;sensei machine learning api
solution: Experience Platform
title: API-slutpunkt för motorer
topic: Developer guide
description: Motorer är grunden för maskininlärningsmodeller i arbetsytan för datavetenskap. De innehåller algoritmer för maskininlärning som löser specifika problem, rörledningar för att utföra funktionsteknik eller bådadera.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---


# Slutpunkt för motorer

Motorer är grunden för maskininlärningsmodeller i arbetsytan för datavetenskap. De innehåller algoritmer för maskininlärning som löser specifika problem, rörledningar för att utföra funktionsteknik eller bådadera.

## Slå upp Docker-registret

>[!TIP]
>
>Om du inte har någon Docker URL går du till självstudiekursen [Paketera källfiler i ett recept](../models-recipes/package-source-files-recipe.md) och får en stegvis genomgång av hur du skapar en Docker-värd-URL.

Docker-registerautentiseringsuppgifterna krävs för att överföra en paketerad mottagarfil, inklusive Docker-värdens URL, användarnamn och lösenord. Du kan söka efter den här informationen genom att utföra följande GET-förfrågan:

**API-format**

```https
GET /engines/dockerRegistry
```

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om Docker-registret inklusive Docker-URL (`host`), användarnamn (`username`) och lösenord (`password`).

>[!NOTE]
>
>Dockerlösenordet ändras när `{ACCESS_TOKEN}` uppdateras.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Skapa en motor med Docker URL:er {#docker-image}

Du kan skapa en motor genom att utföra en begäran om POST samtidigt som du anger dess metadata och en Docker-URL som refererar till en Docker-bild i multipart-formulär.

**API-format**

```https
POST /engines
```

**Begär Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på och kan vara antingen &quot;Python&quot;, &quot;R&quot; eller &quot;Tensorflow&quot;. |
| `algorithm` | En sträng som anger typen av maskininlärningsalgoritm. Algoritmtyper som stöds är Klassificering, Regression eller Custom. |
| `artifacts.default.image.location` | Platsen för dockningsbilden som är länkad till av en Docker-URL. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på och kan vara antingen &quot;Python&quot;, &quot;R&quot; eller &quot;Tensorflow&quot;. |

**Begär PySpark/Scala**

När du begär PySpark-recept är `executionType` och `type`&quot;PySpark&quot;. När du begär ett Scala-recept är `executionType` och `type`&quot;Spark&quot;. I följande exempel på Scala-recept används Spark:

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på. Värdet kan anges till Spark eller PySpark. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. Det här fältet måste anges till `databricks-spark`. |
| `artifacts.default.image.location` | Docker-bildens plats. Endast Azure ACR eller Public (unauthenticated) Dockerhub stöds. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på. Detta kan vara antingen &quot;Spark&quot; eller &quot;PySpark&quot;. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya motorn, inklusive dess unika identifierare (`id`). Följande exempelsvar är för en Python Engine. Alla motorsvar har följande format:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Skapa en rörlig funktionsmotor med Docker URL:er {#feature-pipeline-docker}

Du kan skapa en rörlig funktionsmotor genom att utföra en begäran om POST samtidigt som du anger dess metadata och en Docker-URL som refererar till en Docker-bild.

**API-format**

```https
POST /engines
```

**Begäran**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Egenskap | Beskrivning |
| --- | --- |
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på. Värdet kan anges till Spark eller PySpark. |
| `algorithm` | Den algoritm som används, ange det här värdet till `fp` (funktionspipeline). |
| `name` | Namnet på funktionspipeline-motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. Det här fältet måste anges till `databricks-spark`. |
| `artifacts.default.image.location` | Docker-bildens plats. Endast Azure ACR eller Public (unauthenticated) Dockerhub stöds. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på. Detta kan vara antingen &quot;Spark&quot; eller &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Motorns paketeringstyp. Värdet ska vara `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Konfigurationsfilsparametrarna för `pipeline.json`. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya funktionspipelinmotorn, inklusive dess unika identifierare (`id`). Följande exempelsvar gäller en PySpark-funktionspipelinenmotor.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Hämta en lista med motorer

Du kan hämta en lista över motorer genom att utföra en enda begäran om GET. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista över tillgängliga frågor finns i avsnittet i bilagan [frågeparametrar för hämtning](./appendix.md#query).

**API-format**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista över motorer och deras information.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Hämta en specifik motor {#retrieve-specific}

Du kan hämta information om en viss motor genom att utföra en GET-begäran som innehåller ID:t för den önskade motorn i sökvägen för begäran.

**API-format**

```https
GET /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den önskade motorn.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Uppdatera en motor

Du kan ändra och uppdatera en befintlig motor genom att skriva över dess egenskaper via en PUT-begäran som inkluderar målmotorns ID i sökvägen för begäran och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!NOTE]
>
>För att denna PUT-förfrågan ska lyckas föreslår vi att du först utför en GET-förfrågan om att [hämta motorn med ID](#retrieve-specific). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

Följande exempel på API-anrop uppdaterar en motors namn och beskrivning samtidigt som dessa egenskaper initialt används:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API-format**

```https
PUT /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller den uppdaterade informationen för motorn.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Ta bort en motor

Du kan ta bort en motor genom att utföra en DELETE-begäran och ange målmotorns ID i sökvägen för begäran. Om du tar bort en motor tas alla MLInstances som refererar till den motorn bort, inklusive alla Experiments och Experiment körningar som tillhör dessa MLInstances.

**API-format**

```https
DELETE /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "Engine deletion was successful"
}
```
