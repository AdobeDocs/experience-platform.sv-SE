---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för exportjobb
topic: guide
type: Documentation
description: Med kundprofilen i realtid kan ni skapa en enda bild av enskilda kunder inom Adobe Experience Platform genom att samla data från flera olika källor, både attributdata och beteendedata. Profildata kan sedan exporteras till en datauppsättning för vidare bearbetning.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 0%

---


# Slutpunkt för exportjobb

[!DNL Real-time Customer Profile] Med kan ni skapa en enda vy över enskilda kunder genom att sammanföra data från flera källor, både attributdata och beteendedata. Profildata kan sedan exporteras till en datauppsättning för vidare bearbetning. Till exempel kan målgruppssegment från [!DNL Profile]-data exporteras för aktivering och profilattribut kan exporteras för rapportering.

Det här dokumentet innehåller stegvisa instruktioner för att skapa och hantera exportjobb med [profil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

>[!NOTE]
>
>Den här guiden beskriver användningen av exportjobb i [!DNL Profile API]. Mer information om hur du hanterar exportjobb för Adobe Experience Platform Segmentation Service finns i guiden om [exportjobb i Segmenterings-API](../../profile/api/export-jobs.md).

Förutom att skapa ett exportjobb kan du även komma åt [!DNL Profile]-data med slutpunkten `/entities`, som också kallas [!DNL Profile Access]. Mer information finns i [enheternas slutpunktshandbok](./entities.md). Anvisningar om hur du får åtkomst till [!DNL Profile]-data med användargränssnittet finns i [användarhandboken](../ui/user-guide.md).

## Komma igång

API-slutpunkterna som används i den här guiden är en del av [!DNL Real-time Customer Profile]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform]-API.

## Skapa ett exportjobb

När du exporterar [!DNL Profile]-data måste du först skapa en datauppsättning som data ska exporteras till och sedan starta ett nytt exportjobb. Båda dessa steg kan uppnås med Experience Platform API:er, där den första använder Catalog Service API och den senare med hjälp av Real-time Customer Profile API. Detaljerade instruktioner för hur du slutför varje steg finns i följande avsnitt.

### Skapa en måldatauppsättning

När du exporterar [!DNL Profile]-data måste du först skapa en måldatamängd. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

Ett av de viktigaste övervägandena är schemat som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). För att kunna exportera profildata måste datauppsättningen baseras på unionsschemat [!DNL XDM Individual Profile] (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass. I det här fallet är det klassen [!DNL XDM Individual Profile]. Mer information om unionens vyscheman finns i [facksektionen i grunderna för schemakompositionsguiden](../../xdm/schema/composition.md#union).

Stegen som följer i den här självstudien visar hur du skapar en datauppsättning som refererar till unionsschemat [!DNL XDM Individual Profile] med API:t [!DNL Catalog]. Du kan också använda användargränssnittet [!DNL Platform] för att skapa en datauppsättning som refererar till unionsschemat. Steg för att använda användargränssnittet beskrivs i [den här självstudiekursen för användargränssnitt för att exportera segment](../../segmentation/tutorials/create-dataset-export-segment.md), men kan även användas här. När du är klar kan du gå tillbaka till den här självstudiekursen och fortsätta med stegen för [att starta ett nytt exportjobb](#initiate).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för [att initiera ett nytt exportjobb](#initiate).

**API-format**

```http
POST /dataSets
```

**Begäran**

Följande begäran skapar en ny datauppsättning med konfigurationsparametrar i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true,
          "containerFormat": "parquet",
          "format": "parquet"
        }
      }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett beskrivande namn för datauppsättningen. |
| `schemaRef.id` | ID för den unionsvy (schema) som datauppsättningen ska kopplas till. |
| `fileDescription.persisted` | Ett booleskt värde som när det anges som `true` gör att datauppsättningen kan finnas kvar i unionsvyn. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade, unika ID:t för den nya datauppsättningen. Det krävs ett korrekt konfigurerat datauppsättnings-ID för att profildata ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Initiera exportjobb {#initiate}

När du har en unionskonstanterad datauppsättning kan du skapa ett exportjobb som behåller profildata till datauppsättningen genom att göra en POST till `/export/jobs`-slutpunkten i kundprofils-API:t i realtid och tillhandahålla information om de data som du vill exportera i begärans innehåll.

**API-format**

```http
POST /export/jobs
```

**Begäran**

Följande begäran skapar ett nytt exportjobb med konfigurationsparametrar i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `fields` | *(Valfritt)* Begränsar datafälten som ska inkluderas i exporten till endast de som anges i den här parametern. Om du utelämnar det här värdet inkluderas alla fält i exporterade data. |
| `mergePolicy` | *(Valfritt)* Anger den sammanfogningsprincip som ska användas för att styra exporterade data. Inkludera den här parametern när det finns flera segment som exporteras. |
| `mergePolicy.id` | ID för sammanfogningsprincipen. |
| `mergePolicy.version` | Den specifika versionen av sammanfogningsprincipen som ska användas. Om du utelämnar det här värdet används den senaste versionen som standard. |
| `additionalFields.eventList` | *(Valfritt)* Styr tidsseriens händelsefält som exporteras för underordnade eller associerade objekt genom att ange en eller flera av följande inställningar:<ul><li>`eventList.fields`: Styr fälten som ska exporteras.</li><li>`eventList.filter`: Anger villkor som begränsar resultaten från associerade objekt. Förväntar ett minimivärde som krävs för export, vanligtvis ett datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filtrerar tidsseriehändelser till händelser som har importerats efter den angivna tidsstämpeln. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li></ul> |
| `destination` | **(Obligatoriskt)** Målinformation för exporterade data:<ul><li>`destination.datasetId`:  **(Obligatoriskt)** ID:t för datauppsättningen där data ska exporteras.</li><li>`destination.segmentPerBatch`:  *(Valfritt)* Ett booleskt värde som, om det inte anges, är som standard  `false`. Värdet `false` exporterar alla segment-ID:n till ett enda batch-ID. Värdet `true` exporterar ett segment-ID till ett batch-ID. Observera att om värdet är `true` kan det påverka batchexportens prestanda.</li></ul> |
| `schema.name` | **(Obligatoriskt)** Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |

>[!NOTE]
>
>Om du bara vill exportera profildata och inte inkludera relaterade tidsseriedata tar du bort objektet&quot;additionalFields&quot; från begäran.

**Svar**

Ett lyckat svar returnerar en datauppsättning ifylld med profildata som anges i begäran.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## Visa alla exportjobb

Du kan returnera en lista över alla exportjobb för en viss IMS-organisation genom att utföra en GET-begäran till `export/jobs`-slutpunkten. Begäran stöder också frågeparametrarna `limit` och `offset`, vilket visas nedan.

**API-format**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `start` | Förskjut den returnerade resultatsidan enligt skapandetiden för begäran. Exempel: `start=4` |
| `limit` | Begränsa antalet returnerade resultat. Exempel: `limit=10` |
| `page` | Returnera en specifik resultatsida enligt skapandetiden för begäran. Exempel: `page=2` |
| `sort` | Sortera resultaten efter ett specifikt fält i stigande ( **`asc`**) eller fallande ( **`desc`**) ordning. Sorteringsparametern fungerar inte när flera resultatsidor returneras. Exempel: `sort=updateTime:asc` |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**Svar**

Svaret innehåller ett `records`-objekt som innehåller de exportjobb som har skapats av IMS-organisationen.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## Övervaka exportförlopp

Om du vill visa information om ett specifikt exportjobb, eller övervaka dess status när det bearbetas, kan du göra en GET-förfrågan till `/export/jobs`-slutpunkten och inkludera `id` för exportjobbet i sökvägen. Exportjobbet slutförs när fältet `status` returnerar värdet &quot;SUCCEEDED&quot;.

**API-format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` för det exportjobb som du vill komma åt. |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `batchId` | Identifieraren för de batchar som har skapats från en lyckad export och som ska användas i sökningssyfte vid läsning av profildata. |

## Avbryt ett exportjobb

Med Experience Platform kan du avbryta ett befintligt exportjobb, vilket kan vara användbart av flera anledningar, bland annat om exportjobbet inte slutfördes eller fastnade i bearbetningsfasen. Om du vill avbryta ett exportjobb kan du utföra en DELETE-begäran till `/export/jobs`-slutpunkten och inkludera `id` för det exportjobb som du vill avbryta till sökvägen för begäran.

**API-format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | `id` för det exportjobb som du vill komma åt. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

En borttagningsbegäran returnerar HTTP-status 204 (inget innehåll) och en tom svarstext, vilket anger att åtgärden avbröts.

## Nästa steg

När exporten är klar är dina data tillgängliga i Data Lake i Experience Platform. Du kan sedan använda [API:t för dataåtkomst](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) för att få åtkomst till data med `batchId` som är associerad med exporten. Beroende på exportens storlek kan data vara i segment och gruppen kan bestå av flera filer.

Följ självstudiekursen [Dataåtkomst](../../data-access/tutorials/dataset-data.md) om du vill ha stegvisa anvisningar om hur du använder API:t för dataåtkomst för att få åtkomst till och hämta gruppfiler.

Du kan också komma åt exporterade kundprofildata i realtid med Adobe Experience Platform Query Service. Med API:t UI eller RESTful kan du med Query Service skriva, validera och köra frågor på data i Data Lake.

Mer information om hur du frågar efter målgruppsdata finns i [Query Service-dokumentationen](../../query-service/home.md).

## Bilaga

Följande avsnitt innehåller ytterligare information om exportjobb i profilens API.

### Fler exempel på exportnyttolaster

Exemplet på API-anrop som visas i avsnittet [när ett exportjobb initieras](#initiate) skapar ett jobb som innehåller både profildata (post) och händelsedata (tidsserie). I det här avsnittet finns ytterligare exempel på nyttolasten för begäran som begränsar exporten till att innehålla en datatyp eller en annan.

Följande nyttolast skapar ett exportjobb som bara innehåller profildata (inga händelser):

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

Om du vill skapa ett exportjobb som bara innehåller händelsedata (inga profilattribut) kan nyttolasten se ut ungefär så här:

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### Exportera segment

Du kan också använda slutpunkten för exportjobb för att exportera målgruppssegment i stället för [!DNL Profile]-data. Mer information finns i guiden för [exportjobb i segmenterings-API](../../segmentation/api/export-jobs.md).