---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Motorer
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Motorer

Motorer är grunden för maskininlärningsmodeller i arbetsytan för datavetenskap. De innehåller algoritmer för maskininlärning som löser specifika problem, rörledningar för att utföra funktionsteknik eller bådadera.

## Slå upp Docker-registret

>[!TIP]
>Om du inte har någon Docker-URL kan du gå till [Paketkällfilerna i en recept](../models-recipes/package-source-files-recipe.md) -självstudiekurs för att stegvis gå igenom hur du skapar en Docker-värd-URL.

Docker-registerautentiseringsuppgifterna krävs för att överföra en paketerad mottagarfil, inklusive Docker-värdens URL, användarnamn och lösenord. Du kan söka efter den här informationen genom att utföra följande GET-begäran:

**API-format**

```http
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
>Dockerlösenordet ändras när du `{ACCESS_TOKEN}` uppdaterar.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Skapa en motor med hjälp av Docker URL:er {#docker-image}

Du kan skapa en motor genom att utföra en POST-begäran samtidigt som du anger dess metadata och en Docker-URL som refererar till en Docker-bild i multipart-formulär.

**API-format**

```http
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
                    "location": "{DOCKER_URL}",
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

När en begäran om PySpark-recept görs är `executionType` och `type` &quot;PySpark&quot;. När en begäran om Scala recept görs är `executionType` och `type` &quot;Spark&quot;. I följande exempel på Scala-recept används Spark:

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
    "id": "{ENGINE_ID}",
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
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Hämta en lista med motorer

Du kan hämta en lista över motorer genom att utföra en enda GET-begäran. Du kan filtrera resultaten genom att ange frågeparametrar i sökvägen för begäran. En lista med tillgängliga frågor finns i avsnittet om [frågeparametrar för hämtning](./appendix.md#query)av resurser i bilagan.

**API-format**

```http
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

Du kan hämta information om en specifik motor genom att utföra en GET-begäran som innehåller ID:t för den önskade motorn i sökvägen för begäran.

**API-format**

```http
GET /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den önskade motorn.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Uppdatera en motor

Du kan ändra och uppdatera en befintlig motor genom att skriva över dess egenskaper via en PUT-begäran som inkluderar målmotorns ID i den begärda sökvägen och som tillhandahåller en JSON-nyttolast som innehåller uppdaterade egenskaper.

>[!NOTE] För att säkerställa att denna PUT-begäran lyckas föreslår vi att du först utför en GET-begäran för att [hämta motorn via ID](#retrieve-specific). Ändra och uppdatera sedan det returnerade JSON-objektet och använd hela det ändrade JSON-objektet som nyttolast för PUT-begäran.

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

```http
PUT /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "id": "{ENGINE_ID}",
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

```http
DELETE /engines/{ENGINE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ENGINE_ID}` | ID för en befintlig motor. |

**Begäran**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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

## Föråldrade begäranden

>[!IMPORTANT]
>Binära artefakter stöds inte längre och är inställda på att tas bort vid ett senare datum. Nya PySpark- och Scala-recept bör nu följa [dockningsbildernas](#docker-image) exempel för att skapa en motor.

## Skapa en motor med binära artefakter - borttagen

Du kan skapa en motor med hjälp av lokala `.jar` eller `.egg` binära artefakter genom att utföra en POST-begäran samtidigt som du anger dess metadata och artefaktens sökväg i multipart-formulär.

**API-format**

```http
POST /engines
```

**Begäran**

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
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `algorithm` | En sträng som anger typen av maskininlärningsalgoritm. Algoritmtyper som stöds är Klassificering, Regression eller Custom. |
| `type` | Motorns körningstyp. Det här värdet motsvarar det språk som den binära artefakten bygger på och kan vara antingen&quot;PySpark&quot; eller&quot;Spark&quot;. |


**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya motorn, inklusive dess unika identifierare (`id`).

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Skapa en rörlig motor för funktioner med binära artefakter - borttagen {#create-a-feature-pipeline-engine-using-binary-artifacts}

>[!IMPORTANT]
>Binära artefakter stöds inte längre och är inställda på att tas bort vid ett senare datum.

Du kan skapa en rörlig funktionsmotor med hjälp av lokala `.jar` eller `.egg` binära artefakter genom att utföra en POST-begäran och samtidigt ange dess metadata och artefaktens sökvägar i multipart-formulär. En PySpark- eller Spark-motor kan ange beräkningsresurser, till exempel antalet kärnor eller mängden minne. Mer information finns i bilagan om [resurskonfigurationer](./appendix.md#resource-config) för PySpark och Spark.

**API-format**

```http
POST /engines
```

**Begäran**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `algorithm` | En sträng som anger typen av maskininlärningsalgoritm. Ange det här värdet som &quot;fp&quot; för att ange att det här skapandet ska vara en rörlig funktionsmotor. |
| `type` | Motorns körningstyp. Det här värdet motsvarar det språk som de binära artefakterna bygger på och kan vara antingen&quot;PySpark&quot; eller&quot;Spark&quot;. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya motorn, inklusive dess unika identifierare (`id`).

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```
