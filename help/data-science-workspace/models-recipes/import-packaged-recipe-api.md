---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importera ett paketerat recept (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# Importera ett paketerat recept (API)

I den här självstudiekursen används API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei Machine Learning för att skapa en [motor](../api/engines.md), som också kallas Recept i användargränssnittet.

Innan du börjar är det viktigt att tänka på att Adobe Experience Platform Data Science Workspace använder olika termer för att hänvisa till liknande element i API:t och användargränssnittet. API-termerna används genomgående i den här självstudien och i följande tabell beskrivs motsvarande termer:

| Användargränssnittsterm | API-term |
| ---- | ---- |
| Recipe | [Motor](../api/engines.md) |
| Modell | [MLInstance](../api/mlinstances.md) |
| Utbildning och utvärdering | [Experimentera](../api/experiments.md) |
| Tjänst | [MLService](../api/mlservices.md) |

En motor innehåller maskininlärningsalgoritmer och logik för att lösa specifika problem. I diagrammet nedan visas API-arbetsflödet i arbetsytan Data Science. Den här självstudiekursen fokuserar på att skapa en motor, hjärnan i en maskininlärningsmodell.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Komma igång

Den här självstudien kräver en paketerad mottagarfil i form av antingen en binär artefakt eller en Docker-URL. Följ [paketera källfiler i en Recept](./package-source-files-recipe.md) -självstudiekurs för att skapa en paketerad Recipe-fil eller skapa en egen.

- Binär artefakt: Den binära artefakten (t.ex. JAR, EGG) som används för att skapa en motor.
- `{DOCKER_URL}` : En URL-adress till en Docker-bild av en intelligent tjänst.

I den här självstudiekursen måste du ha slutfört [autentiseringen till Adobe Experience Platform-självstudiekursen](../../tutorials/authentication.md) för att kunna ringa anrop till plattforms-API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, enligt nedan:

- `{ACCESS_TOKEN}`: Ditt specifika värde för innehavartoken som tillhandahålls efter autentisering.
- `{IMS_ORG}`: Dina IMS-organisationsuppgifter finns i din unika integrering med Adobe Experience Platform.
- `{API_KEY}`: Ditt specifika API-nyckelvärde finns i er unika integrering med Adobe Experience Platform.

## Skapa en motor

Beroende på vilken typ av paketerad mottagarfil som ska inkluderas som en del av API-begäran skapas en motor på ett av två sätt:
- [Skapa en motor med en binär artefakt](#create-an-engine-with-a-binary-artifact)
- [Skapa en motor med en Docker URL](#create-an-engine-with-a-docker-url)

### Skapa en motor med en binär artefakt

Om du vill skapa en motor med hjälp av en lokal paketerad `.jar` eller `.egg` binär artefakt måste du ange den absoluta sökvägen till den binära artefaktfilen i det lokala filsystemet. Du kan navigera till katalogen som innehåller den binära artefakten i en Terminal-miljö och köra Unix-kommandot för den absoluta sökvägen. `pwd`

Följande anrop skapar en motor med en binär artefakt:

#### API-format

```http
POST /engines
```

#### Begäran

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` : Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet Data Science Workspace som mottagarens namn.
- `engine > description` : En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i användargränssnittet för datavetenskapen som mottagarens beskrivning. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du väljer att inte ange en beskrivning.
- `engine > type`: Motorns körningstyp. Detta värde motsvarar det språk som den binära artefakten har utvecklats på.

   >[!NOTE] När du överför en binär artefakt för att skapa en motor `type` är antingen `Spark` eller `PySpark`.

- `defaultArtifact` : Den absoluta sökvägen till den binära artefaktfilen som används för att skapa motorn.

   >[!NOTE] Se till att inkludera `@` före filsökvägen.

#### Svar

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

Ett godkänt svar visar en JSON-nyttolast med information om den nya motorn. Nyckeln representerar den unika motoridentifieraren och krävs i nästa självstudie för att skapa en MLInstance. `id` Se till att Engine-identifieraren sparas innan du fortsätter till [nästa steg](#next-steps).

### Skapa en motor med en Docker URL

Om du vill skapa en motor med en paketerad mottagarfil som lagras i en Docker-behållare måste du ange Docker-URL:en till den paketerade mottagarfilen.

Följande anrop skapar en motor med en Docker URL:

#### API-format

```http
POST /engines
```

#### Begäran

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

- `engine > name` : Det önskade namnet på motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i gränssnittet Data Science Workspace som mottagarens namn.
- `engine > description` : En valfri beskrivning av motorn. Mottagaren som motsvarar den här motorn ärver det här värdet som ska visas i användargränssnittet för datavetenskapen som mottagarens beskrivning. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du väljer att inte ange en beskrivning.
- `engine > type`: Motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på.

   >[!NOTE] När en Docker-URL anges för att skapa en motor, `type` är antingen `Python`, `R`eller `Tensorflow`.

- `artifacts > default > image > location` : Din `{DOCKER_URL}` far hit. En komplett Docker-URL har följande struktur:

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` : Ytterligare ett namn för Docker-bildfilen. Ta inte bort den här egenskapen, låt det här värdet vara en tom sträng om du inte anger ett extra namn på Docker-bildfilen.
- `artifacts > default > image > executionType` : Den här motorns körningstyp. Detta värde motsvarar det språk som Docker-bilden har utvecklats på.

   >[!NOTE] När en Docker-URL anges för att skapa en motor, `executionType` är antingen `Python`, `R`eller `Tensorflow`.

#### Svar

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Ett godkänt svar visar en JSON-nyttolast med information om den nya motorn. Nyckeln representerar den unika motoridentifieraren och krävs i nästa självstudie för att skapa en MLInstance. `id` Se till att motorns identifierare sparas innan du fortsätter till nästa steg.

## Nästa steg

Du har skapat en motor med API:t och en unik motoridentifierare har hämtats som en del av svarstexten. Du kan använda den här motoridentifieraren i nästa självstudiekurs när du lär dig hur du [skapar, utbildar och utvärderar en modell med API](./train-evaluate-model-api.md).