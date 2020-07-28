---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Slutpunkt för exportjobb
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 1%

---


# Slutpunkt för exportjobb

Exportjobb är asynkrona processer som används för att behålla målgruppsmedlemmar i datauppsättningar. Du kan använda slutpunkten i API:t för Adobe Experience Platform-segmentering, som gör att du kan hämta, skapa och avbryta exportjobb med programkod. `/export/jobs`

>[!NOTE]
>
>I den här guiden beskrivs hur du använder exportjobb i [!DNL Segmentation API]. Mer information om hur du hanterar exportjobb för [!DNL Real-time Customer Profile] data finns i guiden om [exportjobb i profil-API:t](../../profile/api/export-jobs.md)

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service] API:t. Innan du fortsätter bör du läsa [Komma igång-guiden](./getting-started.md) för att få viktig information som du behöver veta för att kunna anropa API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med exportjobb {#retrieve-list}

Du kan hämta en lista över alla exportjobb för din IMS-organisation genom att göra en GET-förfrågan till `/export/jobs` slutpunkten.

**API-format**

Slutpunkten har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. `/export/jobs` Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla exportjobb som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{LIMIT}` | Anger antalet returnerade exportjobb. |
| `{OFFSET}` | Anger förskjutningen för resultatsidorna. |
| `{STATUS}` | Filtrerar resultaten baserat på status. Värdena som stöds är&quot;NEW&quot;,&quot;SUCCEEDED&quot; och&quot;FAILED&quot;. |

**Begäran**

Följande begäran hämtar de två sista exportjobben inom IMS-organisationen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över slutförda exportjobb, baserat på frågeparametern i sökvägen för begäran.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized", "existing"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `destination` | Målinformation för exporterade data:<ul><li>`datasetId`: ID:t för datauppsättningen där data exporterades.</li><li>`segmentPerBatch`: Ett booleskt värde som visar om segment-ID är konsoliderade eller inte. Värdet &quot;false&quot; innebär att alla segment-ID:n exporteras till ett enda batch-ID. Värdet &quot;true&quot; innebär att ett segment-ID exporteras till ett batch-ID. **Obs!** Om värdet är true kan batchexportens prestanda påverkas.</li></ul> |
| `fields` | En lista med de exporterade fälten, avgränsade med kommatecken. |
| `schema.name` | Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |
| `filter.segments` | Segmenten som exporteras. Följande fält ingår:<ul><li>`segmentId`: Det segment-ID som profiler ska exporteras till.</li><li>`segmentNs`: Segmentnamnutrymme för angiven `segmentID`.</li><li>`status`: En array med strängar som tillhandahåller ett statusfilter för `segmentID`. Som standard `status` har det värde `["realized", "existing"]` som representerar alla profiler som faller inom segmentet vid den aktuella tidpunkten. Möjliga värden är: &quot;real&quot;, &quot;existing&quot; och &quot;exited&quot;.</li></ul> |
| `mergePolicy` | Sammanfoga principinformation för exporterade data. |
| `metrics.totalTime` | Ett fält som anger den totala tiden det tog att köra exportjobbet. |
| `metrics.profileExportTime` | Ett fält som anger den tid det tog för profilerna att exportera. |
| `page` | Information om sidnumreringen av de begärda exportjobben. |
| `link.next` | En länk till nästa sida med exportjobb. |

## Skapa ett nytt exportjobb {#create}

Du kan skapa ett nytt exportjobb genom att göra en POST-förfrågan till `/export/jobs` slutpunkten.

**API-format**

```http
POST /export/jobs
```

**Begäran**

I följande begäran skapas ett nytt exportjobb som konfigurerats med parametrarna i nyttolasten.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `fields` | En lista med de exporterade fälten, avgränsade med kommatecken. Om inget anges exporteras alla fält. |
| `mergePolicy` | Anger den sammanfogningsprincip som ska användas för att styra exporterade data. Inkludera den här parametern när det finns flera segment som exporteras. Om inget anges används samma sammanfogningspolicy som för det angivna segmentet. |
| `filter` | Ett objekt som anger de segment som ska inkluderas i exportjobbet efter ID, kvalificeringstid eller inmatningstid, beroende på de underegenskaper som anges nedan. Om inget anges exporteras alla data. |
| `filter.segments` | Anger de segment som ska exporteras. Om du utelämnar det här värdet exporteras alla data från alla profiler. Accepterar en array med segmentobjekt, där vart och ett innehåller följande fält:<ul><li>`segmentId`: **(Krävs om du använder`segments`)** Segment-ID för profiler som ska exporteras.</li><li>`segmentNs` *(Valfritt)* Segmentnamnutrymme för angiven `segmentID`.</li><li>`status` *(Valfritt)* En array med strängar som tillhandahåller ett statusfilter för `segmentID`. Som standard `status` har det värde `["realized", "existing"]` som representerar alla profiler som faller inom segmentet vid den aktuella tidpunkten. Möjliga värden är: `"realized"`, `"existing"`och `"exited"`.</li></ul> |
| `filter.segmentQualificationTime` | Filtrera baserat på segmentets kvalificeringstid. Starttid och/eller sluttid kan anges. |
| `filter.segmentQualificationTime.startTime` | Starttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på starttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.segmentQualificationTime.endTime` | Sluttid för segmentkvalificering för ett segment-ID för en viss status. Det anges inte, det kommer inte att finnas något filter på sluttiden för ett segment-ID-kvalificering. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. |
| `filter.fromIngestTimestamp ` | Begränsar exporterade profiler till att endast omfatta de som har uppdaterats efter den här tidsstämpeln. Tidsstämpeln måste anges i [RFC 339](https://tools.ietf.org/html/rfc3339) -format. <ul><li>`fromIngestTimestamp` för **profiler**, om sådana finns: Inkluderar alla sammanfogade profiler där den sammanfogade, uppdaterade tidsstämpeln är större än den angivna tidsstämpeln. Stöder `greater_than` operand.</li><li>`fromIngestTimestamp` for **events**: Alla händelser som har importerats efter den här tidsstämpeln exporteras, vilket motsvarar det resulterande profilresultatet. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li> |
| `filter.emptyProfiles` | Ett booleskt värde som anger om tomma profiler ska filtreras. Profiler kan innehålla profilposter, ExperienceEvent-poster eller båda. Profiler utan profilposter och bara ExperienceEvent-poster kallas&quot;emptyProfiles&quot;. Om du vill exportera alla profiler i profilarkivet, inklusive &quot;emptyProfiles&quot;, anger du värdet för `emptyProfiles` till `true`. Om `emptyProfiles` är inställt på `false`exporteras bara profiler med profilposter i butiken. Som standard exporteras bara profiler som innehåller profilposter om attributet inte ingår `emptyProfiles` . |
| `additionalFields.eventList` | Styr tidsseriens händelsefält som exporteras för underordnade eller associerade objekt genom att ange en eller flera av följande inställningar:<ul><li>`fields`: Styr fälten som ska exporteras.</li><li>`filter`: Anger villkor som begränsar resultaten från associerade objekt. Förväntar ett minimivärde som krävs för export, vanligtvis ett datum.</li><li>`filter.fromIngestTimestamp`: Filtrerar tidsseriehändelser till händelser som har importerats efter den angivna tidsstämpeln. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li><li>`filter.toIngestTimestamp`: Filtrerar tidsstämpeln till de som har importerats före den angivna tidsstämpeln. Detta är inte själva händelseläget utan själva intagningstiden för händelserna.</li></ul> |
| `destination` | **(Obligatoriskt)** Information om exporterade data:<ul><li>`datasetId`: **(Obligatoriskt)** ID:t för datauppsättningen där data ska exporteras.</li><li>`segmentPerBatch`: *(Valfritt)* Ett booleskt värde som, om det inte anges, är som standard &quot;false&quot;. Värdet false exporterar alla segment-ID:n till ett enda batch-ID. Värdet true exporterar ett segment-ID till ett batch-ID. Observera att om värdet är &quot;true&quot; kan det påverka batchexportens prestanda.</li></ul> |
| `schema.name` | **(Obligatoriskt)** Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade exportjobb.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Ett systemgenererat skrivskyddat värde som identifierar det exportjobb som just skapades. |

Om du `destination.segmentPerBatch` hade angett `true`det här objektet skulle `destination` ovanstående ha en `batches` array, vilket visas nedan:

```json
    "destination": {
        "dataSetId" : "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches" : [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

## Hämta ett specifikt exportjobb {#get}

Du kan hämta detaljerad information om ett specifikt exportjobb genom att göra en GET-förfrågan till slutpunkten och ange ID:t för det exportjobb som du vill hämta i sökvägen för begäran. `/export/jobs`

**API-format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to access. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna exportjobbet.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{IMS_ORG}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `destination` | Målinformation för exporterade data:<ul><li>`datasetId`: ID:t för datauppsättningen där data exporterades.</li><li>`segmentPerBatch`: Ett booleskt värde som visar om segment-ID är konsoliderade eller inte. Värdet `false` betyder att alla segment-ID:n var i ett enda batch-ID. Värdet `true` betyder att ett segment-ID exporteras till ett batch-ID.</li></ul> |
| `fields` | En lista med de exporterade fälten, avgränsade med kommatecken. |
| `schema.name` | Namnet på schemat som är associerat med datauppsättningen där data ska exporteras. |
| `filter.segments` | Segmenten som exporteras. Följande fält ingår:<ul><li>`segmentId`: Segment-ID för profiler som ska exporteras.</li><li>`segmentNs`: Segmentnamnutrymme för angiven `segmentID`.</li><li>`status`: En array med strängar som tillhandahåller ett statusfilter för `segmentID`. Som standard `status` har det värde `["realized", "existing"]` som representerar alla profiler som faller inom segmentet vid den aktuella tidpunkten. Möjliga värden är: &quot;real&quot;, &quot;existing&quot; och &quot;exited&quot;.</li></ul> |
| `mergePolicy` | Sammanfoga principinformation för exporterade data. |
| `metrics.totalTime` | Ett fält som anger den totala tiden det tog att köra exportjobbet. |
| `metrics.profileExportTime` | Ett fält som anger den tid det tog för profilerna att exportera. |
| `totalExportedProfileCounter` | Det totala antalet profiler som exporterats över alla grupper. |

## Avbryt eller ta bort ett specifikt exportjobb {#delete}

Du kan begära att få ta bort det angivna exportjobbet genom att göra en DELETE-begäran till `/export/jobs` slutpunkten och ange ID:t för det exportjobb som du vill ta bort i sökvägen till begäran.

**API-format**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | The `id` of the export job you want to delete. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 2004 med följande meddelande:

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur exportjobb fungerar.