---
solution: Experience Platform
title: API-slutpunkt för segmentjobb
description: Segmentjobbens slutpunkt i Adobe Experience Platform Segmentation Service API gör att du kan hantera segmentjobb för din organisation programmatiskt.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 0%

---

# Slutpunkt för segmentjobb

Ett segmentjobb är en asynkron process som skapar ett målgruppssegment på begäran. Den refererar till en [segmentdefinition](./segment-definitions.md), samt [sammanfogningsprinciper](../../profile/api/merge-policies.md) styra hur [!DNL Real-Time Customer Profile] sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika typer av information om segmentet, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek.

Den här handboken innehåller information som hjälper dig att förstå segmentjobben bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här guiden är en del av [!DNL Adobe Experience Platform Segmentation Service] API. Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med segmentjobb {#retrieve-list}

Du kan hämta en lista över alla segmentjobb för din organisation genom att göra en GET-förfrågan till `/segment/jobs` slutpunkt.

**API-format**

The `/segment/jobs` slutpunkten har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla exportjobb som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Frågeparametrar**

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade segmentjobben. | `start=1` |
| `limit` | Anger antalet segmentjobb som returneras per sida. | `limit=20` |
| `status` | Filtrerar resultaten baserat på status. Värdena som stöds är NEW, QUEUED, PROCESSING, SUCCEED, FAILED, CANCELING, CANCELING | `status=NEW` |
| `sort` | Beställer de returnerade segmentjobben. Skrivs i formatet `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtrerar segmentjobb och hämtar exakta matchningar för det angivna filtret. Den kan skrivas i något av följande format: <ul><li>`[jsonObjectPath]==[value]` - filtrering på objektnyckeln</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrering i arrayen</li></ul> | `property=segments~segmentId==workInUS` |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över segmentjobb för den angivna organisationen som JSON. Svaret varierar dock beroende på antalet segmentdefinitioner i segmentjobbet.

**Mindre än eller lika med 1 500 segmentdefinitioner i segmentjobbet**

Om du har färre än 1 500 segmentdefinitioner som körs i segmentjobbet visas en fullständig lista över alla segmentdefinitioner i `children.segments` -attribut.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme och visar bara det första returnerade jobbet.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

**Mer än 1 500 segmentdefinitioner**

Om du har fler än 1500 segmentdefinitioner som körs i segmentjobbet kan du `children.segments` attribut kommer att visas `*`, vilket anger att alla segmentdefinitioner utvärderas.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme och visar bara det första returnerade jobbet.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "*",
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet. |
| `status` | Aktuell status för segmentjobbet. Möjliga värden för status är &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; och &quot;SUCCEEDED&quot;. |
| `segments` | Ett objekt som innehåller information om de segmentdefinitioner som returneras i segmentjobbet. |
| `segments.segment.id` | ID för segmentdefinitionen. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |
| `metrics` | Ett objekt som innehåller diagnostikinformation om segmentjobbet. |
| `metrics.totalTime` | Ett objekt som innehåller information om när segmenteringsjobbet påbörjades och avslutades samt den totala tiden. |
| `metrics.profileSegmentationTime` | Ett objekt som innehåller information om de tidpunkter då segmenteringsutvärderingen påbörjades och avslutades samt den totala tiden. |
| `metrics.segmentProfileCounter` | Antalet profiler som kvalificerats per segment. |
| `metrics.segmentedProfileByNamespaceCounter` | Antalet profiler som är kvalificerade för varje identitetsnamnutrymme per segmentdefinitionsbas. |
| `metrics.segmentProfileByStatusCounter` | Antalet profiler för varje status. Följande tre statusvärden stöds: <ul><li>&quot;real&quot; - antalet profiler som kvalificerar sig för segmentdefinitionen.</li><li>&quot;exited&quot; - Antalet profiler som inte längre finns i segmentdefinitionen.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | Det totala antalet sammanfogade profiler per sammanfogningspolicy. |

## Skapa ett nytt segmentjobb {#create}

Du kan skapa ett nytt segmentjobb genom att göra en POST-förfrågan till `/segment/jobs` slutpunkt och inkludera ID:t för segmentdefinitionen som du vill skapa en ny målgrupp från i brödtexten.

**API-format**

```http
POST /segment/jobs
```

När du skapar ett nytt segmentjobb skiljer sig förfrågan och svaret åt beroende på antalet segmentdefinitioner i segmentjobbet.

**Mindre än eller lika med 1 500 segmentdefinitioner i segmentjobbet**

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    }
 ]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentId` | ID:t för segmentdefinitionen som du vill skapa ett segmentjobb för. Dessa segmentdefinitioner kan tillhöra olika sammanfogningsprinciper. Mer information om segmentdefinitioner finns i [slutpunktsguide för segmentdefinition](./segment-definitions.md). |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade segmentjobb.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet som nyligen skapades. |
| `status` | Aktuell status för segmentjobbet. Eftersom segmentjobbet är nyskapat kommer statusen alltid att vara&quot;NYTT&quot;. |
| `segments` | Ett objekt som innehåller information om segmentdefinitionerna som segmentjobbet körs för. |
| `segments.segment.id` | ID:t för segmentdefinitionen som du angav. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |

**Mer än 1 500 segmentdefinitioner**

**Begäran**

>[!NOTE]
>
>Du kan skapa ett segmentjobb med fler än 1 500 segmentdefinitioner, men det här är **rekommenderas inte**.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `schema.name` | Namnet på schemat för segmentdefinitionerna. |
| `segments.segmentId` | När du kör ett segmentjobb med mer än 1 500 segment måste du skicka `*` som det segment-ID som anger att du vill köra ett segmenteringsjobb med alla segment. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade segmentjobb.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet som nyligen skapades. |
| `status` | Aktuell status för segmentjobbet. Eftersom segmentjobbet är nyskapat kommer statusen alltid att vara `NEW`. |
| `segments` | Ett objekt som innehåller information om segmentdefinitionerna som segmentjobbet körs för. |
| `segments.segment.id` | The `*` betyder att segmentjobbet körs för alla segmentdefinitioner i organisationen. |

## Hämta ett specifikt segmentjobb {#get}

Du kan hämta detaljerad information om ett specifikt segmentjobb genom att göra en GET-förfrågan till `/segment/jobs` slutpunkt och ange ID:t för segmentjobbet som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | The `id` värdet för segmentjobbet som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna segmentjobbet.  Svaret varierar dock beroende på antalet segmentdefinitioner i segmentjobbet.

**Mindre än eller lika med 1 500 segmentdefinitioner i segmentjobbet**

Om du har färre än 1 500 segmentdefinitioner som körs i segmentjobbet visas en fullständig lista över alla segmentdefinitioner i `children.segments` -attribut.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

**Mer än 1 500 segmentdefinitioner**

Om du har fler än 1500 segmentdefinitioner som körs i segmentjobbet kan du `children.segments` attribut kommer att visas `*`, vilket anger att alla segmentdefinitioner utvärderas.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "scheduler",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet. |
| `status` | Aktuell status för segmentjobbet. Möjliga värden för status är &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; och &quot;SUCCEEDED&quot;. |
| `segments` | Ett objekt som innehåller information om de segmentdefinitioner som returneras i segmentjobbet. |
| `segments.segment.id` | ID för segmentdefinitionen. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |
| `metrics` | Ett objekt som innehåller diagnostikinformation om segmentjobbet. |

## Masshämta segmentjobb {#bulk-get}

Du kan hämta detaljerad information om flera segmentjobb genom att göra en POST-förfrågan till `/segment/jobs/bulk-get` slutpunkt och tillhandahåller  `id` värden för segmentjobben i begärandetexten.

**API-format**

```http
POST /segment/jobs/bulk-get
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 207 med de begärda segmentjobben. Värdet för `children.segments` Attributet skiljer sig åt beroende på om segmentjobbet körs för mer än 1 500 segmentdefinitioner.

>[!NOTE]
>
>Följande svar har trunkerats för blanksteg och visar bara en del av informationen för varje segmentjobb. Det fullständiga svaret innehåller fullständig information om de begärda segmentjobben.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "*"
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet. |
| `status` | Aktuell status för segmentjobbet. Möjliga värden för status är &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; och &quot;SUCCEEDED&quot;. |
| `segments` | Ett objekt som innehåller information om de segmentdefinitioner som returneras i segmentjobbet. |
| `segments.segment.id` | ID för segmentdefinitionen. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |

## Avbryt eller ta bort ett specifikt segmentjobb {#delete}

Du kan ta bort ett specifikt segmentjobb genom att göra en DELETE-förfrågan till `/segment/jobs` slutpunkt och ange ID:t för segmentjobbet som du vill ta bort i sökvägen för begäran.

>[!NOTE]
>
>API-svaret på borttagningsbegäran är omedelbart. Den faktiska borttagningen av segmentjobbet är dock asynkron. Det finns med andra ord en tidsskillnad mellan när en raderingsbegäran görs för segmentjobbet och när det tillämpas.

**API-format**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | The `id` värdet för segmentjobbet som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 med följande information.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur segmentjobb fungerar.
