---
solution: Experience Platform
title: API-slutpunkt för segmentdefinitioner
description: Med segmentdefinitionsslutpunkten i Adobe Experience Platform Segmentation Service API kan du programmässigt hantera segmentdefinitioner för din organisation.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: 424702d7d16eddabefe19d023c3829bd650c88ce
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# Slutpunkt för segmentdefinitioner

>[!WARNING]
>
>Skapande av målgrupper med B2B-enheter med segmenteringstjänstens API är föråldrat. Du kan inte längre skapa målgrupper med hjälp av följande B2B-enheter: Konto, Kontorelation, Kampanj, Kampanjmedlem, Marknadsföringslista, Marknadsföringslistmedlem, Affärsmöjlighet och Person-relation.

Med Adobe Experience Platform kan du skapa segmentdefinitioner som definierar en grupp med specifika attribut eller beteenden från en grupp profiler. En segmentdefinition är ett objekt som kapslar in en fråga skriven i [!DNL Profile Query Language] (PQL). Segmentdefinitioner används på profiler för att skapa målgrupper. Det här objektet (segmentdefinitionen) kallas också för ett PQL-predikat. PQL förutsäger regler för segmentdefinitionen baserat på villkor som relaterar till alla post- eller tidsseriedata som du skickar till [!DNL Real-Time Customer Profile]. Mer information om hur du skriver PQL-frågor finns i [PQL-handboken](../pql/overview.md).

Den här handboken innehåller information som hjälper dig att förstå segmentdefinitioner bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hämta en lista med segmentdefinitioner {#list}

Du kan hämta en lista över alla segmentdefinitioner för din organisation genom att göra en GET-begäran till slutpunkten `/segment/definitions`.

**API-format**

Slutpunkten `/segment/definitions` har stöd för flera frågeparametrar som kan hjälpa dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader. Om du anropar den här slutpunkten utan parametrar hämtas alla segmentdefinitioner som är tillgängliga för organisationen. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Frågeparametrar**

+++ En lista med tillgängliga frågeparametrar.

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Anger startförskjutningen för de returnerade segmentdefinitionerna. | `start=4` |
| `limit` | Anger antalet segmentdefinitioner som returneras per sida. | `limit=20` |
| `page` | Anger vilken sida som resultatet av segmentdefinitioner ska börja från. | `page=5` |
| `sort` | Anger vilket fält som resultaten ska sorteras efter. Har skrivits i följande format: `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Anger om segmentdefinitionen är direktuppspelningsaktiverad. | `evaluationInfo.continuous.enabled=true` |

+++

**Begäran**

Följande begäran hämtar de två sista segmentdefinitionerna som publicerats i organisationen.

+++ En exempelbegäran om att hämta en lista med segmentdefinitioner.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över segmentdefinitioner för den angivna organisationen som JSON.

+++ Ett exempelsvar när en lista med segmentdefinitioner hämtas.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

+++

## Skapa en ny segmentdefinition {#create}

Du kan skapa en ny segmentdefinition genom att göra en POST-begäran till slutpunkten `/segment/definitions`.

>[!IMPORTANT]
>
>Segmentdefinitioner som har skapats med API:t **kan inte** redigeras med segmentverktyget.

**API-format**

```http
POST /segment/definitions
```

**Begäran**

När du skapar en ny segmentdefinition kan du skapa den i formatet `pql/text` eller `pql/json`.

>[!BEGINTABS]

>[!TAB Använda pql/text]

+++ En exempelbegäran om att skapa en segmentdefinition.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett unikt namn som ska referera till segmentdefinitionen. |
| `description` | (Valfritt) En beskrivning av segmentdefinitionen som du skapar. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara &quot;PQL&quot;. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Värden som stöds är `pql/text` och `pql/json`. |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `evaluationInfo` | (Valfritt) Den typ av segmentdefinition som du skapar. Om du vill skapa ett gruppsegment anger du `evaluationInfo.batch.enabled` som true. Om du vill skapa ett direktuppspelningssegment anger du `evaluationInfo.continuous.enabled` som true. Om du vill skapa ett kantsegment anger du `evaluationInfo.synchronous.enabled` som true. Om segmentdefinitionen lämnas tom skapas den som ett **batch**-segment. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id`- eller `name`-fält. |

+++

>[!TAB Använder pql/json]

+++ En exempelbegäran om att skapa en segmentdefinition.

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
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Ett unikt namn som ska referera till segmentdefinitionen. |
| `description` | (Valfritt) En beskrivning av segmentdefinitionen som du skapar. |
| `evaluationInfo` | (Valfritt) Den typ av segmentdefinition som du skapar. Om du vill skapa ett gruppsegment anger du `evaluationInfo.batch.enabled` som true. Om du vill skapa ett direktuppspelningssegment anger du `evaluationInfo.continuous.enabled` som true. Om du vill skapa ett kantsegment anger du `evaluationInfo.synchronous.enabled` som true. Om segmentdefinitionen lämnas tom skapas den som ett **batch**-segment. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id`- eller `name`-fält. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara &quot;PQL&quot;. |
| `expression.format` | Anger strukturen för uttrycket i värdet. |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |

+++

>[!ENDTABS]

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den segmentdefinition du nyss skapade.

+++ Ett exempelsvar när du skapar en segmentdefinition.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `evaluationInfo` | Ett objekt som anger vilken typ av utvärdering som segmentdefinitionen ska genomgå. Det kan vara gruppsegmentering, direktuppspelning (kallas även kontinuerlig) eller kantsegmentering (kallas även synkron). |

+++

## Hämta en specifik segmentdefinition {#get}

Du kan hämta detaljerad information om en specifik segmentdefinition genom att göra en GET-begäran till slutpunkten `/segment/definitions` och ange ID:t för segmentdefinitionen som du vill hämta i sökvägen till begäran.

**API-format**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | Värdet `id` för segmentdefinitionen som du vill hämta. |

**Begäran**

+++ En exempelbegäran om att hämta en segmentdefinition.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna segmentdefinitionen.

+++ Ett exempelsvar när en segmentdefinition hämtas.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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
| `name` | Ett unikt namn som ska referera till segmentdefinitionen. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id`- eller `name`-fält. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara &quot;PQL&quot;. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `description` | En läsbar beskrivning av definitionen. |
| `evaluationInfo` | Ett objekt som anger vilken typ av utvärdering, batch, direktuppspelning (kallas även kontinuerlig) eller kant (kallas även synkron), kommer segmentdefinitionen att genomgå. |

+++

## Hämta segmentdefinitioner gruppvis {#bulk-get}

Du kan hämta detaljerad information om flera angivna segmentdefinitioner genom att göra en POST-begäran till `/segment/definitions/bulk-get`-slutpunkten och ange `id`-värdena för segmentdefinitionerna i begärandetexten.

**API-format**

```http
POST /segment/definitions/bulk-get
```

**Begäran**

+++ En exempelbegäran när du använder bulkens get-slutpunkt.

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

| Egenskap | Beskrivning |
| -------- | ----------- |
| `ids` | En array som innehåller objekt som anger ID:n för de segmentdefinitioner som du vill hämta. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 207 med de begärda segmentdefinitionerna.

+++ Ett samplingssvar när du använder bulkens get-slutpunkt.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
| `name` | Ett unikt namn som ska referera till segmentdefinitionen. |
| `schema` | Det schema som är associerat med entiteterna i segmentet. Består av antingen ett `id`- eller `name`-fält. |
| `expression` | En entitet som innehåller fältinformation om segmentdefinitionen. |
| `expression.type` | Anger uttryckstypen. För närvarande stöds bara &quot;PQL&quot;. |
| `expression.format` | Anger strukturen för uttrycket i värdet. Följande format stöds för närvarande: <ul><li>`pql/text`: En textbeteckning för en segmentdefinition enligt den publicerade PQL-grammatiken.  Exempel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ett uttryck som överensstämmer med typen som anges i `expression.format`. |
| `description` | En läsbar beskrivning av definitionen. |
| `evaluationInfo` | Ett objekt som anger vilken typ av utvärdering, batch, direktuppspelning (kallas även kontinuerlig) eller kant (kallas även synkron), kommer segmentdefinitionen att genomgå. |

+++

## Ta bort en specifik segmentdefinition {#delete}

Du kan begära att få ta bort en viss segmentdefinition genom att göra en DELETE-begäran till `/segment/definitions`-slutpunkten och ange ID:t för segmentdefinitionen som du vill ta bort i sökvägen till begäran.

>[!NOTE]
>
> En segmentdefinition som används i målaktiveringen **kan inte tas bort**.

**API-format**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | Värdet `id` för segmentdefinitionen som du vill ta bort. |

**Begäran**

+++ En exempelbegäran om att ta bort en segmentdefinition.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 utan något meddelande.

## Uppdatera en specifik segmentdefinition

Du kan uppdatera en specifik segmentdefinition genom att göra en PATCH-begäran till slutpunkten `/segment/definitions` och ange ID:t för segmentdefinitionen som du vill uppdatera i sökvägen till begäran.

**API-format**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{SEGMENT_ID}` | Värdet `id` för segmentdefinitionen som du vill uppdatera. |

**Begäran**

Följande begäran kommer att uppdatera arbetsadresslandet från USA till Kanada.

>[!NOTE]
>
>Eftersom det här API-anropet **ersätter** innehållet i segmentdefinitionen måste du se till att **alla** fält som du vill behålla ingår i begärandetexten.

+++ Ett exempel på en begäran om att uppdatera en segmentdefinition.

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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nyligen uppdaterade segmentdefinitionen.

+++ Ett exempelsvar när en segmentdefinition uppdateras.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

+++

## Konvertera segmentdefinition

Du kan konvertera en segmentdefinition mellan `pql/text` och `pql/json` eller `pql/json` till `pql/text` genom att göra en POST-begäran till `/segment/conversion`-slutpunkten.

**API-format**

```http
POST /segment/conversion
```

**Begäran**

Följande begäran ändrar segmentdefinitionens format från `pql/text` till `pql/json`.

+++ En exempelbegäran om att konvertera segmentdefinitionen.

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
        "payloadSchema": "string"
    }'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om din nyligen konverterade segmentdefinition.

+++ Ett samplingssvar när segmentdefinitionen konverteras.

```json
{
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

+++

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur segmentdefinitioner fungerar. Mer information om hur du skapar ett segment finns i självstudiekursen [Skapa ett segment](../tutorials/create-a-segment.md).
