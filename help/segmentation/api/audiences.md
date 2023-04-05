---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;målgrupper;målgrupp;API;api;
title: Målgrupps-API-slutpunkt
description: Målgruppsslutpunkten i Adobe Experience Platform Segmentation Service API gör att ni kan hantera målgrupper för er organisation programmatiskt.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
hide: true
hidefromtoc: true
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 0%

---

# Målgruppsslutpunkt

>[!IMPORTANT]
>
>Målgruppens slutpunkt är för närvarande i betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

En publik är en samling personer som har liknande beteenden och/eller egenskaper. Dessa samlingar med personer kan genereras antingen med Adobe Experience Platform eller från externa källor. Du kan använda `/audiences` -slutpunkten i segmenterings-API, som gör att du kan hämta, skapa, uppdatera och ta bort målgrupper med programkod.

## Komma igång

Slutpunkterna som används i den här guiden är en del av [!DNL Adobe Experience Platform Segmentation Service] API. Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med målgrupper {#list}

Du kan hämta en lista över alla målgrupper för din organisation genom att göra en GET-förfrågan till `/audiences` slutpunkt.

**API-format**

The `/audiences` slutpunkten har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader när du listar resurser. Om du anropar den här slutpunkten utan parametrar hämtas alla målgrupper som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Följande frågeparametrar kan användas när en lista över målgrupper hämtas:

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade målgrupperna. | `start=5` |
| `limit` | Anger det maximala antalet målgrupper som returneras per sida. | `limit=10` |
| `sort` | Anger den ordning som resultaten ska sorteras efter. Detta skrivs i formatet `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Ett filter som gör att du kan ange målgrupper som **exakt** matchar ett attributvärde. Detta skrivs i formatet `property=` | `property=audienceId==test-audience-id` |
| `name` | Ett filter som gör att du kan ange målgrupper vars namn **innehåller** det angivna värdet. Det här värdet är inte skiftlägeskänsligt. | `name=Sample` |
| `description` | Ett filter som gör att du kan ange målgrupper vars beskrivningar **innehåller** det angivna värdet. Det här värdet är inte skiftlägeskänsligt. | `description=Test Description` |
| `withMetrics` | Ett filter som returnerar mätvärden utöver målgrupperna. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>För målgrupper returneras mätvärden under `metrics` och innehåller information om antal profiler, hur tidsstämplar skapas och uppdateras.

**Inga mått**

Följande par med begäran/svar används när `withMetrics` frågeparametern finns inte.

**Begäran**

Följande begäran hämtar de fem senaste målgrupperna som skapats i din organisation.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Svar** {#no-metrics}

Ett lyckat svar returnerar HTTP-status 200 med en lista över målgrupper som skapats i din organisation som JSON.

>[!NOTE]
>
>Följande svar har trunkerats för space och visar endast den första målgruppen som returneras.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Egenskap | Målgruppstyp | Beskrivning |
| -------- | ------------- | ----------- | 
| `id` | Båda | En systemgenererad skrivskyddad identifierare för målgruppen. |
| `audienceId` | Båda | Om målgruppen är en plattformsgenererad målgrupp är detta samma värde som `id`. Om målgruppen genereras externt anges det här värdet av klienten. |
| `schema` | Båda | Målgruppens XDM-schema (Experience Data Model). |
| `imsOrgId` | Båda | ID för organisationen som målgruppen tillhör. |
| `sandbox` | Båda | Information om sandlådan som målgruppen tillhör. Mer information om sandlådor finns i [översikt över sandlådor](../../sandboxes/home.md). |
| `name` | Båda | Publiken. |
| `description` | Båda | En beskrivning av publiken. |
| `expression` | Plattformsgenererad | PQL-uttrycket (Profile Query Language) för målgruppen. Mer information om PQL-uttryck finns i [Guide för PQL-uttryck](../pql/overview.md). |
| `mergePolicyId` | Plattformsgenererad | ID för den sammanfogningsprincip som målgruppen är kopplad till. Mer information om kopplingsprofiler finns i [guide för sammanslagningsprinciper](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Plattformsgenererad | Visar hur målgruppen kommer att utvärderas. Möjliga bedömningsmetoder är batch, streaming eller edge. Mer information om utvärderingsmetoderna finns i [segmenteringsöversikt](../home.md) |
| `dependents` | Båda | En array med målgrupps-ID:n som är beroende av den aktuella målgruppen. Detta används om du skapar en målgrupp som är ett segment i ett segment. |
| `dependencies` | Båda | En array med målgrupps-ID:n som målgruppen är beroende av. Detta används om du skapar en målgrupp som är ett segment i ett segment. |
| `type` | Båda | Ett systemgenererat fält som visar om publiken genereras av plattformen eller är en externt genererad publik. Möjliga värden är `SegmentDefinition` och `ExternalAudience`. A `SegmentDefinition` avser en publik som genererats i Platform, medan en `ExternalAudience` avser en publik som inte genererats i Platform. |
| `createdBy` | Båda | ID för den användare som skapade målgruppen. |
| `labels` | Båda | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |
| `namespace` | Båda | Det namnutrymme som målgruppen tillhör. Möjliga värden är `AAM`, `AAMSegments`, `AAMTraits`och `AEPSegments`. |
| `audienceMeta` | Extern | Externt skapade metadata från externt skapade målgrupper. |

**Med mätvärden**

Följande par med begäran/svar används när `withMetrics` frågeparametern finns.

**Begäran**

Följande begäran hämtar de fem senaste målgrupperna, med mätvärden, som skapats i din organisation.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över målgrupper, med mätvärden, för den angivna organisationen som JSON.

>[!NOTE]
>
>Följande svar har trunkerats för space och visar endast den första målgruppen som returneras.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "realized": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

Följande listegenskaper **exklusiv** till `withMetrics` svar. Om du vill veta mer om standardmålgruppsegenskaperna kan du läsa [föregående avsnitt](#no-metrics).

| Egenskap | Beskrivning |
| -------- | ----------- |
| `metrics.imsOrgId` | Målgruppens organisations-ID. |
| `metrics.sandbox` | Sandlådeinformationen som är relaterad till målgruppen. |
| `metrics.jobId` | ID:t för segmentjobbet som bearbetar målgruppen. |
| `metrics.type` | Segmentjobbtypen. Detta kan antingen vara `export` eller `batch_segmentation`. |
| `metrics.id` | Målgruppens ID. |
| `metrics.data` | Mätvärden som är relaterade till publiken. Detta inkluderar information som det totala antalet profiler som ingår i målgruppen, det totala antalet profiler per namnområde och det totala antalet profiler per status. |
| `metrics.createEpoch` | En tidsstämpel som visas när målgruppen skapades. |
| `metrics.updateEpoch` | En tidsstämpel som visas när målgruppen senast uppdaterades. |

## Skapa en ny målgrupp {#create}

Du kan skapa en ny målgrupp genom att göra en förfrågan om POST till `/audiences` slutpunkt.

**API-format**

```http
POST /audiences
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `name` | Publiken. |
| `description` | En beskrivning av publiken. |
| `type` | Ett fält som visar om målgruppen är plattformsgenererad eller är en externt genererad målgrupp. Möjliga värden är `SegmentDefinition` och `ExternalAudience`. A `SegmentDefinition` avser en publik som genererats i Platform, medan en `ExternalAudience` avser en publik som inte genererats i Platform. |
| `expression` | PQL-uttrycket (Profile Query Language) för målgruppen. Mer information om PQL-uttryck finns i [Guide för PQL-uttryck](../pql/overview.md). |
| `schema` | Målgruppens XDM-schema (Experience Data Model). |
| `labels` | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |

**Svar**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Söka efter en viss målgrupp {#get}

Du kan söka efter detaljerad information om en viss målgrupp genom att göra en GET-förfrågan till `/audiences` slutpunkt och ange ID för den målgrupp som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parameter | Beskrivning |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | ID:t för den målgrupp du försöker hämta. |
| `property=withmetrics==true` | En valfri frågeparameter som du kan använda om du vill hämta en angiven målgrupp med målgruppsmåtten. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna målgruppen. Svaret varierar beroende på om målgruppen genereras med Adobe Experience Platform eller externa källor.

**Plattformsgenererad**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Externt genererad**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Uppdatera ett fält i en målgrupp {#update-field}

Du kan uppdatera fälten för en viss målgrupp genom att göra en PATCH-förfrågan till `/audiences` slutpunkt och ange ID för den målgrupp som du vill uppdatera i sökvägen för begäran.

**API-format**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID:t för den målgrupp som du vill uppdatera. |

**Begäran**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `op` | För uppdatering av målgrupper är det här värdet alltid `add`. |
| `path` | Sökvägen till det fält som du vill uppdatera. |
| `value` | Värdet som du vill uppdatera fältet till. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade målgruppen.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Uppdatera en målgrupp {#put}

Du kan uppdatera (skriva över) en viss målgrupp genom att göra en PUT-förfrågan till `/audiences` slutpunkt och ange ID för den målgrupp som du vill uppdatera i sökvägen för begäran.

**API-format**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Begäran**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `audienceId` | Målgruppens ID. Detta används av externa målgrupper |
| `name` | Publiken. |
| `namespace` |  |
| `description` | En beskrivning av publiken. |
| `type` | Ett systemgenererat fält som visar om publiken genereras av plattformen eller är en externt genererad publik. Möjliga värden är `SegmentDefinition` och `ExternalAudience`. A `SegmentDefinition` avser en publik som genererats i Platform, medan en `ExternalAudience` avser en publik som inte genererats i Platform. |
| `lifecycle` | Status för målgruppen. Möjliga värden är `draft`, `published`, `inactive`och `archived`. `draft` representerar när målgruppen skapas, `published` när målgruppen publiceras, `inactive` när målgruppen inte längre är aktiv, och `archived` om målgruppen tas bort. |
| `datasetId` | ID:t för datauppsättningen som målgruppsdata kan hittas. |
| `labels` | Dataanvändning på objektnivå och attributbaserade etiketter för åtkomstkontroll som är relevanta för publiken. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nya uppdaterade målgrupp. Observera att informationen om er målgrupp varierar beroende på om det är en plattformsgenererad publik eller en externt genererad målgrupp.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Ta bort en målgrupp {#delete}

Du kan ta bort en viss målgrupp genom att göra en DELETE-förfrågan till `/audiences` slutpunkt och ange ID för den målgrupp som du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{AUDIENCE_ID}` | ID:t för den målgrupp som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 utan något meddelande.
