---
keywords: Experience Platform;hem;populära ämnen;övervaka dataflöden;flödestjänst api;Flödestjänst
solution: Experience Platform
title: Övervaka dataflöden med API:t för flödestjänsten
topic-legacy: overview
type: Tutorial
description: Den här självstudiekursen beskriver stegen för övervakning av körningsdata för flöde för fullständighet, fel och mätvärden med API:t för Flow Service.
exl-id: 5b7d1aa4-5e6d-48f4-82bd-5348dc0e890d
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# Övervaka dataflöden med API:t för Flow Service

I den här självstudiekursen beskrivs stegen för övervakning av körningsdata för flöde för fullständighet, fel och mätvärden med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>I den här självstudiekursen måste du ha ID-värdet för ett giltigt dataflöde. Om du inte har ett giltigt dataflödes-ID väljer du den önskade anslutningen på menyn [källöversikt](../../home.md) och följ instruktionerna för att skapa ett dataflöde innan du provar den här självstudiekursen.

## Komma igång

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Övervaka dataflöden

Om du vill se dataflödets status skickar du en GET-förfrågan till [!DNL Flow Service] API, samtidigt som du anger ditt dataflödes-ID.

**API-format**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för det dataflöde som du vill övervaka. |

**Begäran**

Följande begäran hämtar specifikationerna för ett befintligt dataflöde.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om flödets körning, inklusive information om dess skapandedatum, käll- och målanslutningar samt flödets unika identifierare (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "c9cef9cb-c934-4467-8ef9-cbc934546741",
            "etag": "\"b8003af1-0000-0200-0000-5f2b09f10000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `items` | Innehåller en enda nyttolast av metadata som är associerade med din specifika flödeskörning. |
| `metrics` | Definierar egenskaper för data i flödeskörningen. |
| `activities` | Definierar hur data omformas. |
| `durationSummary` | Definierar start- och sluttiden för flödeskörningen. |
| `sizeSummary` | Definierar datavolymen i byte. |
| `recordSummary` | Definierar antalet poster i data. |
| `fileSummary` | Definierar antalet filer för data. |
| `statusSummary` | Definierar om flödeskörningen är en lyckad eller misslyckad åtgärd. |

## Nästa steg

Genom att följa den här självstudiekursen har du hämtat statistik och felinformation om ditt dataflöde med hjälp av [!DNL Flow Service] API. Du kan nu fortsätta att övervaka ditt dataflöde, beroende på ditt intag, för att spåra dess status och intag. Information om hur du utför samma uppgifter med användargränssnittet finns i självstudiekursen om [övervaka dataflöden med användargränssnittet](../ui/monitor.md)
