---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;segmentdefinition;segmentdefinitioner;api;API;
solution: Experience Platform
title: API-slutpunkt för segmentdefinitioner
description: Med segmentdefinitionsslutpunkten i Adobe Experience Platform Segmentation Service API kan du programmässigt hantera segmentdefinitioner för din organisation.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Slutpunkt för segmentdefinitioner

Med Adobe Experience Platform kan du skapa segment som definierar en grupp med specifika attribut eller beteenden från en grupp profiler. En segmentdefinition är ett objekt som kapslar in en fråga skriven i [!DNL Profile Query Language] (PQL). Det här objektet kallas även för ett PQL-predikat. PQL-predikat definierar reglerna för segmentet baserat på villkor som relaterar till data från poster eller tidsserier som du skickar till [!DNL Real-Time Customer Profile]. Se [PQL-guide](../pql/overview.md) om du vill ha mer information om hur du skriver PQL-frågor.

Den här handboken innehåller information som hjälper dig att förstå segmentdefinitioner bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här guiden är en del av [!DNL Adobe Experience Platform Segmentation Service] API. Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med segmentdefinitioner {#list}

Du kan hämta en lista över alla segmentdefinitioner för din IMS-organisation genom att göra en GET-förfrågan till `/segment/definitions` slutpunkt.

**API-format**

The `/segment/definitions` slutpunkten har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla segmentdefinitioner som är tillgängliga för organisationen. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Frågeparametrar**

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade segmentdefinitionerna. | `start=4` |
| `limit` | Anger antalet segmentdefinitioner som returneras per sida. | `limit=20` |
| `page` | Anger vilken sida som resultatet av segmentdefinitioner ska börja från. | `page=5` |
| `sort` | Anger vilket fält som resultaten ska sorteras efter. Skrivs i följande format: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Anger om segmentdefinitionen är direktuppspelningsaktiverad. | `evaluationInfo.continuous.enabled=true` |

**Begäran**

Följande begäran hämtar de två sista segmentdefinitionerna som publicerats i IMS-organisationen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över segmentdefinitioner för den angivna IMS-organisationen som JSON.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Skapa en ny segmentdefinition {#create}

Du kan skapa en ny segmentdefinition genom att göra en POST-förfrågan till `/segment/definitions` slutpunkt.

**API-format**

```http
POST /segment/definitions
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | **Obligatoriskt.** Ett unikt namn som ska referera till segmentet. |
| `schema` | **Obligatoriskt.** Det schema som är associerat med entiteterna i segmentet. Består av antingen en `id` eller `name` fält. |
| `expression` | **Obligatoriskt.** En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara PQL. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `description` | En läsbar beskrivning av definitionen. |

>[!NOTE]
>
>Ett segmentdefinitionsuttryck kan också referera till ett beräknat attribut. Mer information finns i [API-slutpunktshandbok för beräknat attribut](../../profile/computed-attributes/ca-api.md)
>
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den segmentdefinition du nyss skapade.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Ett systemgenererat ID för den segmentdefinition du nyss skapade. |
| `evaluationInfo` | Ett systemgenererat objekt som anger vilken typ av utvärdering som segmentdefinitionen ska genomgå. Den kan vara en grupp, kontinuerlig (kallas även direktuppspelning) eller synkron segmentering. |

## Hämta en specifik segmentdefinition {#get}

Du kan hämta detaljerad information om en viss segmentdefinition genom att göra en GET-förfrågan till `/segment/definitions` slutpunkt och ange ID:t för segmentdefinitionen som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | The `id` värdet för segmentdefinitionen som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna segmentdefinitionen.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Ett systemgenererat skrivskyddat ID för segmentdefinitionen. |
| `name` | Ett unikt namn som ska referera till segmentet. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen en `id` eller `name` fält. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara PQL. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `description` | En läsbar beskrivning av definitionen. |
| `evaluationInfo` | Ett systemgenererat objekt som anger vilken typ av utvärdering, batch, kontinuerlig (kallas även direktuppspelning) eller synkron, segmentdefinitionen ska genomgå. |

## Hämta segmentdefinitioner gruppvis {#bulk-get}

Du kan hämta detaljerad information om flera angivna segmentdefinitioner genom att göra en POST-förfrågan till `/segment/definitions/bulk-get` slutpunkt och tillhandahåller `id` värden för segmentdefinitionerna i begärandetexten.

**API-format**

```http
POST /segment/definitions/bulk-get
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 207 med de begärda segmentdefinitionerna.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Ett systemgenererat skrivskyddat ID för segmentdefinitionen. |
| `name` | Ett unikt namn som ska referera till segmentet. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen en `id` eller `name` fält. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara PQL. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `description` | En läsbar beskrivning av definitionen. |
| `evaluationInfo` | Ett systemgenererat objekt som anger vilken typ av utvärdering, batch, kontinuerlig (kallas även direktuppspelning) eller synkron, segmentdefinitionen ska genomgå. |

## Ta bort en specifik segmentdefinition {#delete}

Du kan begära att få ta bort en viss segmentdefinition genom att göra en DELETE-förfrågan till `/segment/definitions` slutpunkt och ange ID:t för segmentdefinitionen som du vill ta bort i sökvägen för begäran.

>[!NOTE]
>
> Du kommer att **not** kan ta bort ett segment som används i en målaktivering.

**API-format**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | The `id` värdet för segmentdefinitionen som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 utan något meddelande.

## Uppdatera en specifik segmentdefinition

Du kan uppdatera en specifik segmentdefinition genom att göra en PATCH-begäran till `/segment/definitions` slutpunkt och ange ID:t för segmentdefinitionen som du vill uppdatera i sökvägen för begäran.

**API-format**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | The `id` värdet för segmentdefinitionen som du vill uppdatera. |

**Begäran**

Följande begäran kommer att uppdatera arbetsadresslandet från USA till Kanada.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade segmentdefinitionen. Lägg märke till hur arbetsadresslandet har uppdaterats från USA (USA) till Kanada (CA).

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Konvertera segmentdefinition

Du kan konvertera en segmentdefinition mellan `pql/text` och `pql/json` eller `pql/json` till `pql/text` genom att göra en POST-förfrågan till `/segment/conversion` slutpunkt.

**API-format**

```http
POST /segment/conversion
```

**Begäran**

Följande begäran ändrar segmentdefinitionens format från `pql/text` till `pql/json`.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nyligen konverterade segmentdefinition.

```json
{
    "ttlInDays": 60,
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur segmentdefinitioner fungerar. Mer information om hur du skapar ett segment finns i [skapa ett segment](../tutorials/create-a-segment.md) självstudiekurs.
