---
keywords: Experience Platform;import packaged recept;Data Science Workspace;populära topics;recipes;api;sensei machine learning;create engine
solution: Experience Platform
title: Importera en paketerad mottagare med Sensei Machine Learning API
type: Tutorial
description: I den här självstudien används API:t för inlärning i Sensei Machine för att skapa en motor, som också kallas Recept i användargränssnittet.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Importera ett paketerat recept med Sensei Machine Learning API

I den här självstudiekursen används [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) för att skapa [Motor](../api/engines.md), kallas även Recept i användargränssnittet.

Innan du börjar är det viktigt att tänka på att Adobe Experience Platform [!DNL Data Science Workspace] använder olika termer för att referera till liknande element i API och användargränssnitt. API-termerna används genomgående i den här självstudien och i följande tabell beskrivs motsvarande termer:

| Användargränssnittsterm | API-term |
| ---- | ---- |
| Recipe | [Motor](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Utbildning och utvärdering | [Experimentera](../api/experiments.md) |
| Tjänst | [MLService](../api/mlservices.md) |

En motor innehåller maskininlärningsalgoritmer och logik för att lösa specifika problem. I bilden nedan visas API-arbetsflödet i [!DNL Data Science Workspace]. Den här självstudiekursen fokuserar på att skapa en motor, hjärnan i en maskininlärningsmodell.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Komma igång

Den här självstudien kräver en paketerad mottagarfil i form av en Docker-URL. Följ [Paketera källfiler i en mottagare](./package-source-files-recipe.md) självstudiekurs för att skapa en paketerad mottagarfil eller skapa en egen.

- `{DOCKER_URL}`: En URL-adress till en Docker-bild av en intelligent tjänst.

Den här självstudiekursen kräver att du har slutfört [Autentisering till Adobe Experience Platform, självstudiekurs](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] API:er. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

- `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{ORG_ID}`: Dina IMS-organisationsuppgifter finns i din unika Adobe Experience Platform-integrering.
- `{API_KEY}`: Ditt specifika API-nyckelvärde som finns i din unika Adobe Experience Platform-integrering.

## Skapa en motor

Du kan skapa motorer genom att göra en POST-förfrågan till slutpunkten /engines. Den skapade motorn konfigureras baserat på den paketerade mottagarfilen som måste inkluderas som en del av API-begäran.

### Skapa en motor med en Docker URL {#create-an-engine-with-a-docker-url}

Om du vill skapa en motor med en paketerad mottagarfil som lagras i en Docker-behållare måste du ange Docker-URL:en till den paketerade mottagarfilen.

>[!CAUTION]
>
> Om du använder [!DNL Python] eller R använder begäran nedan. Om du använder PySpark eller Scala ska du använda exemplet på PySpark/Scala-begäran som finns under Python/R-exemplet.

**API-format**

```http
POST /engines
```

**Begär Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Egenskap | Beskrivning |
| -------  | ----------- |
| `engine.name` | Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i [!DNL Data Science Workspace] som mottagarens namn. |
| `engine.description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i [!DNL Data Science Workspace] som mottagarens beskrivning. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du väljer att inte ange en beskrivning. |
| `engine.type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på. När en Docker URL anges för att skapa en motor, `type` är antingen `Python`, `R`, `PySpark`, `Spark` (Scala), eller `Tensorflow`. |
| `artifacts.default.image.location` | Dina `{DOCKER_URL}` går hit. En komplett Docker-URL har följande struktur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Ytterligare ett namn för Docker-bildfilen. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du inte anger ett extra namn på Docker-bildfilen. |
| `artifacts.default.image.executionType` | Den här motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på. När en Docker URL anges för att skapa en motor, `executionType` är antingen `Python`, `R`, `PySpark`, `Spark` (Scala), eller `Tensorflow`. |

**Begär PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;PySpark&quot;. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. |
| `artifacts.default.image.location` | Platsen för dockningsbilden som är länkad till av en Docker-URL. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |

**Request Scala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. |
| `artifacts.default.image.location` | Platsen för dockningsbilden som är länkad till av en Docker-URL. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya motorn, inklusive dess unika identifierare (`id`). Följande exempelsvar är för en [!DNL Python] Motor. The `executionType` och `type` ändras baserat på angiven POST.

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

Ett godkänt svar visar en JSON-nyttolast med information om den nya motorn. The `id` -nyckeln representerar den unika motoridentifieraren och krävs i nästa självstudie för att skapa en MLInstance. Se till att motorns identifierare sparas innan du fortsätter till nästa steg.

## Nästa steg {#next-steps}

Du har skapat en motor med API:t och en unik motoridentifierare har hämtats som en del av svarstexten. Du kan använda den här motoridentifieraren i nästa självstudiekurs när du lär dig hur du [skapa, utbilda och utvärdera en modell med API:t](./train-evaluate-model-api.md).
