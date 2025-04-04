---
keywords: Experience Platform;importera paketerat recept;Data Science Workspace;populära topics;recipes;api;sensei machine learning;skapa motor
solution: Experience Platform
title: Importera en paketerad mottagare med Sensei Machine Learning API
type: Tutorial
description: I den här självstudien används API:t för inlärning i Sensei Machine för att skapa en motor, som också kallas Recept i användargränssnittet.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 0%

---

# Importera ett paketerat recept med Sensei Machine Learning API

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa.
>
>Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

I den här självstudien används [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) för att skapa en [motor](../api/engines.md) som också kallas recept i användargränssnittet.

Innan du börjar är det viktigt att tänka på att Adobe Experience Platform [!DNL Data Science Workspace] använder olika termer för att referera till liknande element i API:t och användargränssnittet. API-termerna används genomgående i den här självstudien och i följande tabell beskrivs motsvarande termer:

| Användargränssnittsterm | API-term |
| ---- | ---- |
| Recipe | [Motor](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Utbildning och utvärdering | [Experimentera](../api/experiments.md) |
| Tjänst | [MLService](../api/mlservices.md) |

En motor innehåller maskininlärningsalgoritmer och logik för att lösa specifika problem. I diagrammet nedan visas API-arbetsflödet i [!DNL Data Science Workspace]. Den här självstudiekursen fokuserar på att skapa en motor, hjärnan i en maskininlärningsmodell.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Komma igång

Den här självstudien kräver en paketerad mottagarfil i form av en Docker-URL. Följ [Paketera källfiler i en recept](./package-source-files-recipe.md)-självstudiekurs för att skapa en paketerad mottagarfil eller skapa en egen.

- `{DOCKER_URL}`: En URL-adress till en Docker-bild av en intelligent tjänst.

Den här självstudien kräver att du har slutfört [autentiseringen av Adobe Experience Platform-självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Experience Platform] API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken har angetts efter autentiseringen.
- `{ORG_ID}`: Dina organisationsuppgifter hittades i din unika Adobe Experience Platform-integrering.
- `{API_KEY}`: Ditt specifika API-nyckelvärde hittades i din unika Adobe Experience Platform-integrering.

## Skapa en motor

Du kan skapa motorer genom att göra en POST-begäran till slutpunkten /engines. Den skapade motorn konfigureras baserat på den paketerade mottagarfilen som måste inkluderas som en del av API-begäran.

### Skapa en motor med en Docker URL {#create-an-engine-with-a-docker-url}

Om du vill skapa en motor med en paketerad mottagarfil som lagras i en Docker-behållare måste du ange Docker-URL:en till den paketerade mottagarfilen.

>[!CAUTION]
>
> Om du använder [!DNL Python] eller R använder du begäran nedan. Om du använder PySpark eller Scala ska du använda exemplet på PySpark/Scala-begäran som finns under Python/R-exemplet.

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
| `engine.name` | Namnet på motorn som du vill använda. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i [!DNL Data Science Workspace]-användargränssnittet som mottagarens namn. |
| `engine.description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i användargränssnittet för [!DNL Data Science Workspace] som mottagarens beskrivning. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du väljer att inte ange en beskrivning. |
| `engine.type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på. När en Docker URL anges för att skapa en motor är `type` antingen `Python`, `R`, `PySpark`, `Spark` (Skala) eller `Tensorflow`. |
| `artifacts.default.image.location` | Din `{DOCKER_URL}` är här. En fullständig Docker-URL har följande struktur: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Ytterligare ett namn för Docker-bildfilen. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du inte anger ett extra namn på Docker-bildfilen. |
| `artifacts.default.image.executionType` | Den här motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på. När en Docker URL anges för att skapa en motor är `executionType` antingen `Python`, `R`, `PySpark`, `Spark` (Skala) eller `Tensorflow`. |

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
| `name` | Namnet på motorn som du vill använda. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i användargränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på PySpark. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. |
| `artifacts.default.image.location` | Platsen för dockningsbilden som är länkad till av en Docker-URL. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |

**Begär scala**

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
| `name` | Namnet på motorn som du vill använda. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet som mottagarens namn. |
| `description` | En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i användargränssnittet som mottagarens beskrivning. Den här egenskapen är obligatorisk. Om du inte vill ange en beskrivning anger du värdet som en tom sträng. |
| `type` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |
| `mlLibrary` | Ett fält som krävs när du skapar motorer för PySpark- och Scala-recept. |
| `artifacts.default.image.location` | Platsen för dockningsbilden som är länkad till av en Docker-URL. |
| `artifacts.default.image.executionType` | Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden bygger på &quot;Spark&quot;. |

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller information om den nya motorn, inklusive dess unika identifierare (`id`). Följande exempelsvar är för en [!DNL Python]-motor. Nycklarna `executionType` och `type` ändras baserat på den angivna POST.

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

Ett lyckat svar visar en JSON-nyttolast med information om den nya motorn. Nyckeln `id` representerar den unika motoridentifieraren och krävs i nästa självstudie för att skapa en MLInstance. Se till att Engine-identifieraren sparas innan du fortsätter till nästa steg.

## Nästa steg {#next-steps}

Du har skapat en motor med API:t och en unik motoridentifierare har hämtats som en del av svarstexten. Du kan använda den här motoridentifieraren i nästa självstudie när du lär dig hur du [skapar, utbildar och utvärderar en modell med API](./train-evaluate-model-api.md).
