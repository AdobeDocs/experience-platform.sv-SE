---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Exportera data med API:er
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---


# Exportera profildata med API:er

Med kundprofilen i realtid kan ni skapa en enda vy över enskilda kunder genom att samla data från flera olika källor, både attributdata och beteendedata. Data som är tillgängliga i profilen kan sedan exporteras till en datauppsättning för vidare bearbetning. Den här självstudiekursen innehåller stegvisa instruktioner för att skapa och hantera exportjobb med [segmenterings-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Förutom att skapa ett exportjobb kan du även komma åt profildata med hjälp av API:t för profilåtkomst och genom projektioner. Se självstudiekursen [om API för](../../profile/api/entities.md) profilåtkomst eller självstudiekursen om hur du [konfigurerar kantmål och prognoser](../../profile/api/edge-projections.md) för mer information om dessa andra åtkomstmönster.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som används för att arbeta med profildata. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
- [Segmenteringstjänsten](../home.md)Adobe Experience Platform: Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.
- [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Obligatoriska rubriker

Den här självstudiekursen kräver även att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna ringa anrop till Platform API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla POST-, PUT- och PATCH-begäranden kräver ytterligare en rubrik:

- Innehållstyp: application/json

## Skapa ett exportjobb

För att kunna exportera profildata måste du först skapa en datauppsättning som data ska exporteras till och sedan starta ett nytt exportjobb. Båda dessa steg kan uppnås med Experience Platform API:er, där den första använder Catalog Service API och den senare med hjälp av Real-time Customer Profile API. Detaljerade instruktioner för hur du slutför varje steg finns i följande avsnitt.

- [Skapa en måldatauppsättning](#create-a-target-dataset) - Skapa en datauppsättning för exporterade data.
- [Initiera ett nytt exportjobb](#initiate-export-job) - Fyll i datauppsättningen med XDM-data för enskild profil.

### Skapa en måldatauppsättning

När du exporterar profildata måste du först skapa en måldatauppsättning. Det är viktigt att datauppsättningen är korrekt konfigurerad för att exporten ska lyckas.

En av de viktigaste sakerna att tänka på är det schema som datauppsättningen baseras på (`schemaRef.id` i API-exempelbegäran nedan). För att kunna exportera ett segment måste datauppsättningen baseras på XDM Individual Profile Union Schema (`https://ns.adobe.com/xdm/context/profile__union`). Ett unionsschema är ett systemgenererat, skrivskyddat schema som samlar in fält i scheman som delar samma klass, i det här fallet klassen XDM Individual Profile. Mer information om unionsvyscheman finns i avsnittet Kundprofil i [realtid i Utvecklarhandbok](../../xdm/schema/composition.md#union)för schemaregister.

De steg som följer i den här självstudien beskriver hur du skapar en datauppsättning som refererar till XDM-schemat för enskilda profiler med hjälp av katalog-API:t. Du kan också använda användargränssnittet i Adobe Experience Platform för att skapa en datauppsättning som refererar till unionsschemat. Steg för att använda användargränssnittet beskrivs i [den här självstudiekursen för användargränssnitt för att exportera segment](./create-dataset-export-segment.md) , men kan även användas här. När du är klar kan du gå tillbaka till den här självstudiekursen och fortsätta med stegen för att [starta ett nytt exportjobb](#initiate-export-job).

Om du redan har en kompatibel datauppsättning och känner till dess ID kan du fortsätta direkt till steget för att [initiera ett nytt exportjobb](#initiate-export-job).

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
| `fileDescription.persisted` | Ett booleskt värde som, när det anges till `true`, gör att datauppsättningen kan finnas kvar i unionsvyn. |

**Svar**

Ett lyckat svar returnerar en array som innehåller det skrivskyddade, systemgenererade, unika ID:t för den nya datauppsättningen. Det krävs ett korrekt konfigurerat datauppsättnings-ID för att profildata ska kunna exporteras.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Initiera exportjobb

När du har en unionskonstanterad datauppsättning kan du skapa ett exportjobb som behåller profildata till datauppsättningen genom att göra en POST-begäran till `/export/jobs` slutpunkten i kundprofils-API:t i realtid och tillhandahålla information om de data som du vill exportera i huvuddelen av begäran.

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `fields` | *(Valfritt)* Begränsar datafälten som ska inkluderas i exporten till endast de som anges i den här parametern. Samma parameter är också tillgänglig när du skapar ett segment, och därför kan fälten i segmentet redan ha filtrerats. Om du utelämnar det här värdet inkluderas alla fält i exporterade data. |
| `mergePolicy` | *(Valfritt)* Anger vilken sammanfogningsprincip som ska styra exporterade data. Inkludera den här parametern när det finns flera segment som exporteras. Om det här värdet utelämnas används den sammanslagningsprincip som tillhandahålls av segmentet. |
| `mergePolicy.id` | ID för sammanfogningsprincipen. |
| `mergePolicy.version` | Den specifika versionen av sammanfogningsprincipen som ska användas. Om du utelämnar det här värdet används den senaste versionen som standard. |
| `filter` | *(Valfritt)* Anger ett eller flera av följande filter som ska användas på segmentet före export. |
| `filter.segments` | *(Valfritt)* Anger vilka segment som ska exporteras. Om du utelämnar det här värdet exporteras alla data från alla profiler. Accepterar en array med segmentobjekt, där vart och ett innehåller följande fält:<ul><li>`segmentId`: **(Krävs om du använder`segments`)** Segment-ID för profiler som ska exporteras.</li><li>`segmentNs` *(Valfritt)* Segmentnamnutrymme för angiven `segmentID`.</li><li>`status` *(Valfritt)* En array med strängar som tillhandahåller ett statusfilter för `segmentID`. Som standard `status` har det värde `["realized", "existing"]` som representerar alla profiler som faller inom segmentet vid den aktuella tidpunkten. Möjliga värden är: `"realized"`, `"existing"`och `"exited"`.</br></br>Mer information finns i självstudiekursen [Skapa segment](./create-a-segment.md).</li></ul> |
| `filter.segmentQualificationTime` | *(Valfritt)* Filtrera baserat på segmentets kvalificeringstid. Starttid och/eller sluttid kan anges. |
| `filter.segmentQualificationTime.startTime` | *(Valfritt)* Starttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på starttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.segmentQualificationTime.endTime` | *(Valfritt)* Sluttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på sluttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.fromIngestTimestamp ` | *(Valfritt)* Begränsar exporterade profiler till att endast omfatta de som har uppdaterats efter den här tidsstämpeln. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. <ul><li>`fromIngestTimestamp` för **profiler**, om sådana finns: Inkluderar alla sammanfogade profiler där den sammanfogade, uppdaterade tidsstämpeln är större än den angivna tidsstämpeln. Stöder `greater_than` operand.</li><li>`fromTimestamp` for **events**: Alla händelser som har importerats efter den här tidsstämpeln exporteras, vilket motsvarar det resulterande profilresultatet. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li> |
| `filter.emptyProfiles` | *(Valfritt)* Boolean. Profiler kan innehålla profilposter, ExperienceEvent-poster eller båda. Profiler utan profilposter och bara ExperienceEvent-poster kallas&quot;emptyProfiles&quot;. Om du vill exportera alla profiler i profilarkivet, inklusive &quot;emptyProfiles&quot;, anger du värdet för `emptyProfiles` till `true`. Om `emptyProfiles` är inställt på `false`exporteras bara profiler med profilposter i butiken. Som standard exporteras bara profiler som innehåller profilposter om attributet inte ingår `emptyProfiles` . |
| `additionalFields.eventList` | *(Valfritt)* Styr tidsseriens händelsefält som exporteras för underordnade eller associerade objekt genom att ange en eller flera av följande inställningar:<ul><li>`eventList.fields`: Styr fälten som ska exporteras.</li><li>`eventList.filter`: Anger villkor som begränsar resultaten från associerade objekt. Förväntar ett minimivärde som krävs för export, vanligtvis ett datum.</li><li>`eventList.filter.fromIngestTimestamp`: Filtrerar händelser för tidsserier till händelser som har importerats efter den angivna tidsstämpeln. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li></ul> |
| `destination` | **(Obligatoriskt)** Målinformation för exporterade data:<ul><li>`destination.datasetId`: **(Obligatoriskt)** ID:t för datauppsättningen där data ska exporteras.</li><li>`destination.segmentPerBatch`: *(Valfritt)* Ett booleskt värde som, om det inte anges, är som standard `false`. Värdet för `false` exporterar alla segment-ID:n till ett enda batch-ID. Värdet för `true` exporterar ett segment-ID till ett batch-ID. Observera att om du anger värdet som ska `true` påverkas batchexportens prestanda.</li></ul> |
| `schema.name` | **(Obligatoriskt)** Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |
| `evaluationInfo.segmentation` | *(Valfritt)* Ett booleskt värde som, om det inte anges, är som standard `false`. Värdet är `true` att segmentering måste göras i exportjobbet. |

>[!NOTE]
>
>Om du bara vill exportera profildata, och inte inkludera relaterade ExperienceEvent-data, tar du bort objektet&quot;additionalFields&quot; från begäran.

**Svar**

Ett lyckat svar returnerar en datauppsättning ifylld med profildata som anges i begäran.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Om `destination.segmentPerBatch` inte hade tagits med i begäran (om den inte fanns, var den som standard `false`) eller om värdet hade angetts till `false`, skulle `destination` objektet i svaret ovan inte ha någon `batches` array och i stället bara innehålla en `batchId`, vilket visas nedan. Den enskilda batchen skulle innehålla alla segment-ID, medan svaret ovan visar ett enda segment-ID per batch-ID.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

## Visa alla exportjobb

Du kan returnera en lista över alla exportjobb för en viss IMS-organisation genom att utföra en GET-begäran till `export/jobs` slutpunkten. Begäran stöder också frågeparametrarna `limit` och `offset`enligt nedan.

**API-format**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `limit` | Ange antalet poster som ska returneras. |
| `offset` | Förskjut resultatsidan som ska returneras av det angivna numret. |

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

Svaret innehåller ett `records` objekt som innehåller de exportjobb som har skapats av IMS-organisationen.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

Om du vill visa information om ett specifikt exportjobb, eller övervaka statusen när det bearbetas, kan du göra en GET-begäran till `/export/jobs` slutpunkten och inkludera `id` exportjobbets status i sökvägen. Exportjobbet slutförs när `status` fältet returnerar värdet &quot;SUCCEEDED&quot;.

**API-format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

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
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
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

Med Experience Platform kan du avbryta ett befintligt exportjobb, vilket kan vara användbart av flera anledningar, bland annat om exportjobbet inte slutfördes eller fastnade i bearbetningsfasen. Om du vill avbryta ett exportjobb kan du utföra en DELETE-begäran till `/export/jobs` slutpunkten och inkludera den del `id` av exportjobbet som du vill avbryta till begärandesökvägen.

**API-format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

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

När exporten är klar är dina data tillgängliga i Data Lake i Experience Platform. Du kan sedan använda API:t [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dataåtkomst för att komma åt data med hjälp av de `batchId` som är kopplade till exporten. Beroende på exportens storlek kan data vara i segment och gruppen kan bestå av flera filer.

Följ självstudiekursen ( [Data Access) om du vill ha stegvisa anvisningar om hur du använder API:t för dataåtkomst för att få åtkomst till och hämta gruppfiler](../../data-access/tutorials/dataset-data.md).

Du kan också komma åt exporterade kundprofildata i realtid med Adobe Experience Platform Query Service. Med API:t UI eller RESTful kan du med Query Service skriva, validera och köra frågor på data i Data Lake.

Mer information om hur du frågar efter målgruppsdata finns i dokumentationen [för](../../query-service/home.md)frågetjänsten.