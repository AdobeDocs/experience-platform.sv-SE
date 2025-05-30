---
solution: Experience Platform
title: API-slutpunkt för segmentjobb
description: Segmentjobbens slutpunkt i Adobe Experience Platform Segmentation Service API gör att du kan hantera segmentjobb för din organisation programmatiskt.
role: Developer
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: 9eb5ccc24db58a887473f61c66a83aa92e16efa7
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# Slutpunkt för segmentjobb

Ett segmentjobb är en asynkron process som skapar ett målgruppssegment på begäran. Den refererar till en [segmentdefinition](./segment-definitions.md) samt alla [sammanfogningsprinciper](../../profile/api/merge-policies.md) som styr hur [!DNL Real-Time Customer Profile] sammanfogar överlappande attribut i dina profilfragment. När ett segmentjobb har slutförts kan du samla in olika typer av information om segmentet, t.ex. eventuella fel som kan ha inträffat under bearbetningen och målgruppens slutliga storlek.

Den här handboken innehåller information som hjälper dig att förstå segmentjobben bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med segmentjobb {#retrieve-list}

Du kan hämta en lista över alla segmentjobb för din organisation genom att göra en GET-begäran till slutpunkten `/segment/jobs`.

**API-format**

Slutpunkten `/segment/jobs` har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla exportjobb som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**Frågeparametrar**

+++ En lista med tillgängliga frågeparametrar.

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade segmentjobben. | `start=1` |
| `limit` | Anger antalet segmentjobb som returneras per sida. | `limit=20` |
| `status` | Filtrerar resultaten baserat på status. Värdena som stöds är NEW, QUEUED, PROCESSING, SUCCEED, FAILED, CANCELING, CANCELING | `status=NEW` |
| `sort` | Beställer returnerade segmentjobb. Har skrivits i formatet `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | Filtrerar segmentjobb och hämtar exakta matchningar för angivet filter. Den kan skrivas i något av följande format: <ul><li>`[jsonObjectPath]==[value]` - filtrering på objektnyckeln</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - filtrering i arrayen</li></ul> | `property=segments~segmentId==workInUS` |

+++

**Begäran**

+++ Ett exempel på en begäran om att visa en lista med segmentjobb.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över segmentjobb för den angivna organisationen som JSON. En fullständig lista över alla segmentdefinitioner visas i attributet `children.segments`.

>[!NOTE]
>
>Följande svar har trunkerats för utrymme och visar bara det första returnerade jobbet.

+++ Ett exempelsvar när en lista över segmentjobb hämtas.

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

+++

## Skapa ett nytt segmentjobb {#create}

Du kan skapa ett nytt segmentjobb genom att göra en POST-begäran till `/segment/jobs`-slutpunkten och inkludera ID:n för segmentdefinitionen i begärandetexten.

**API-format**

```http
POST /segment/jobs
```

**Begäran**

+++En exempelbegäran för att skapa ett nytt segmentjobb

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
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `segmentId` | ID:t för segmentdefinitionen som du vill utvärdera. Dessa segmentdefinitioner kan tillhöra olika sammanfogningsprinciper. Mer information om segmentdefinitioner finns i [stödlinjen för segmentdefinitioner](./segment-definitions.md). |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen skapade segmentjobb.

+++ Ett exempelsvar när du skapar ett nytt segmentjobb.

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
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
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
| `status` | Aktuell status för segmentjobbet. Eftersom segmentjobbet är nyskapat blir alltid statusen&quot;NYTT&quot;. |
| `segments` | Ett objekt som innehåller information om segmentdefinitionerna som segmentjobbet körs för. |
| `segments.segment.id` | ID:t för segmentdefinitionen som du angav. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |

+++

## Hämta ett specifikt segmentjobb {#get}

Du kan hämta detaljerad information om ett specifikt segmentjobb genom att göra en GET-begäran till slutpunkten `/segment/jobs` och ange ID:t för segmentjobbet som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Värdet `id` för segmentjobbet som du vill hämta. |

**Begäran**

+++ En exempelbegäran för hämtning av ett segmentjobb.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna segmentjobbet. En fullständig lista över alla segmentdefinitioner visas i attributet `children.segments`.

+++ Ett exempelsvar för hämtning av ett segmentjobb.

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

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | En systemgenererad skrivskyddad identifierare för segmentjobbet. |
| `status` | Aktuell status för segmentjobbet. Möjliga värden för status är &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; och &quot;SUCCEEDED&quot;. |
| `segments` | Ett objekt som innehåller information om de segmentdefinitioner som returneras i segmentjobbet. |
| `segments.segment.id` | ID för segmentdefinitionen. |
| `segments.segment.expression` | Ett objekt som innehåller information om segmentdefinitionens uttryck, skrivet i PQL. |
| `metrics` | Ett objekt som innehåller diagnostikinformation om segmentjobbet. |

+++

>[!ENDTABS]

## Masshämta segmentjobb {#bulk-get}

Du kan hämta detaljerad information om flera segmentjobb genom att göra en POST-begäran till `/segment/jobs/bulk-get`-slutpunkten och ange `id`-värdena för segmentjobben i begärandetexten.

**API-format**

```http
POST /segment/jobs/bulk-get
```

**Begäran**

+++ En exempelbegäran för användning av bulkhämtningsslutpunkten.

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

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 207 med de begärda segmentjobben.

>[!NOTE]
>
>Följande svar har trunkerats för blanksteg och visar bara en del av informationen för varje segmentjobb. Det fullständiga svaret innehåller fullständig information om de begärda segmentjobben.

+++ Ett samplingssvar när gruppsvaret används.

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
                    "segmentId": "30230300-d78c-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-d78c-48ad-8012-c5563a007069",
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

+++

## Avbryt eller ta bort ett specifikt segmentjobb {#delete}

Du kan ta bort ett specifikt segmentjobb genom att göra en DELETE-begäran till slutpunkten `/segment/jobs` och ange ID:t för segmentjobbet som du vill ta bort i begärandesökvägen.

>[!NOTE]
>
>API-svaret på borttagningsbegäran är omedelbart. Den faktiska borttagningen av segmentjobbet är dock asynkron. Det finns med andra ord en tidsskillnad mellan när en raderingsbegäran görs för segmentjobbet och när det tillämpas.

**API-format**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | Värdet `id` för segmentjobbet som du vill ta bort. |

**Begäran**

+++ En exempelbegäran om att ta bort ett segmentjobb.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 204 med en tom svarstext.

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur segmentjobb fungerar.
