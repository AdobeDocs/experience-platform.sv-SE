---
keywords: Experience Platform;hem;populära ämnen;Politiska åtgärder;Automatisk tillsyn;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: API-slutpunkter för principutvärdering
description: När marknadsföringsåtgärder har skapats och principer har definierats, kan du använda API:t för principtjänsten för att utvärdera om några profiler överträds av vissa åtgärder. De returnerade begränsningarna har formen av en uppsättning principer som skulle överträdas om marknadsföringsåtgärden utförs på de angivna data som innehåller dataanvändningsetiketter.
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---

# Slutpunkter för principutvärdering

När marknadsföringsåtgärder har skapats och dataanvändningspolicyer har definierats kan du använda [!DNL Policy Service] API för att utvärdera om några profiler överträds av vissa åtgärder. De returnerade begränsningarna har formen av en uppsättning principer som skulle överträdas om marknadsföringsåtgärden utförs på de angivna data som innehåller dataanvändningsetiketter.

Som standard är det bara profiler vars status är inställd på `ENABLED` delta i utvärderingen. Du kan dock använda frågeparametern `?includeDraft=true` att inkludera `DRAFT` Utvärderingsprinciper.

Begäran om utvärdering kan göras på ett av tre sätt:

1. Brottar åtgärden mot några policyer med tanke på en marknadsföringsåtgärd och en uppsättning etiketter för dataanvändning?
1. Om en marknadsföringsåtgärd och en eller flera datauppsättningar utförs, bryter åtgärden mot några policyer?
1. Om en marknadsföringsåtgärd, en eller flera datauppsättningar och en deluppsättning av ett eller flera fält i var och en av dessa datauppsättningar, bryter åtgärden mot några policyer?

## Komma igång

API-slutpunkterna som används i den här handboken är en del av [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Innan du fortsätter bör du granska [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anrop i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna ringa anrop till [!DNL Experience Platform] API.

## Utvärdera för policyöverträdelser med hjälp av dataanvändningsetiketter {#labels}

Du kan utvärdera om det finns principöverträdelser baserat på en viss uppsättning dataanvändningsetiketter med hjälp av `duleLabels` frågeparameter i en GET-begäran.

**API-format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på marknadsföringsåtgärden som ska testas mot en uppsättning dataanvändningsetiketter. Du kan hämta en lista över tillgängliga marknadsföringsåtgärder genom att skapa en [GET-begäran till slutpunkten för marknadsföringsåtgärder](./marketing-actions.md#list). |
| `{LABELS_LIST}` | En kommaavgränsad lista med namn på dataanvändningsetiketter som marknadsföringsåtgärden ska testas mot. Till exempel: `duleLabels=C1,C2,C3`<br><br>Observera att etikettnamn är skiftlägeskänsliga. Se till att du använder rätt skiftläge när du listar dem i `duleLabels` parameter. |

**Begäran**

Exemplet nedan utvärderar en marknadsföringsåtgärd mot etiketterna C1 och C3.

>[!IMPORTANT]
>
>Var medveten om `AND` och `OR` -operatorer i dina policyuttryck. I exemplet nedan, om någon av etiketterna`C1` eller `C3`) hade framträtt ensam i begäran och marknadsföringsåtgärden skulle inte ha brutit mot denna policy. Det krävs båda etiketterna (`C1` och `C3`) för att återlämna den felaktiga policyn. Se till att ni utvärderar policyer noggrant och definierar politiska uttryck med lika stor omsorg.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar innehåller `violatedPolicies` array, som innehåller detaljerna om de policyer som överträtts som ett resultat av marknadsföringsåtgärden mot de angivna etiketterna. Om inga policyer överträds `violatedPolicies` matrisen kommer att vara tom.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Utvärdera för policyöverträdelser med datauppsättningar {#datasets}

Du kan utvärdera om det finns principfel baserat på en uppsättning med en eller flera datauppsättningar från vilka dataanvändningsetiketter kan samlas in. Detta gör du genom att göra en POST till `/constraints` slutpunkt för en specifik marknadsföringsåtgärd och tillhandahålla en lista med datauppsättnings-ID:n i begärandetexten.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på marknadsföringsåtgärden som ska testas mot en eller flera datauppsättningar. Du kan hämta en lista över tillgängliga marknadsföringsåtgärder genom att skapa en [GET-begäran till slutpunkten för marknadsföringsåtgärder](./marketing-actions.md#list). |

**Begäran**

Följande begäran utför `crossSiteTargeting` marknadsföringsåtgärder mot en uppsättning av tre datauppsättningar som ska utvärderas för eventuella policyöverträdelser.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `entityType` | Typen av enhet vars ID anges i jämställda `entityId` -egenskap. För närvarande är det enda godkända värdet `dataSet`. |
| `entityId` | ID:t för en datauppsättning som marknadsföringsåtgärden ska testas mot. En lista över datauppsättningar och deras motsvarande ID:n kan hämtas genom att en GET-begäran görs till `/dataSets` slutpunkt i [!DNL Catalog Service] API. Se guiden på [lista [!DNL Catalog] objekt](../../catalog/api/list-objects.md) för mer information. |

**Svar**

Ett lyckat svar innehåller `violatedPolicies` -array, som innehåller detaljer om de principer som överträtts som ett resultat av att marknadsföringsåtgärden utfördes mot de angivna datauppsättningarna. Om inga policyer överträds `violatedPolicies` matrisen kommer att vara tom.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{ORG_ID}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `duleLabels` | Responsobjektet innehåller en `duleLabels` en array som innehåller en konsoliderad lista med alla etiketter som finns i de angivna datauppsättningarna. Den här listan innehåller datauppsättnings- och fältnivåetiketter för alla fält i datauppsättningen. |
| `discoveredLabels` | Svaret innehåller även en `discoveredLabels` array som innehåller objekt för varje datamängd, visa `datasetLabels` uppdelat i etiketter på datamängd- och fältnivå. Varje etikett på fältnivå visar sökvägen till det specifika fältet med den etiketten. |

## Utvärdera för policyöverträdelser med hjälp av specifika datauppsättningsfält {#fields}

Du kan utvärdera om det finns principfel som baseras på en delmängd av fält i en eller flera datauppsättningar, så att endast de dataanvändningsetiketter som används för dessa fält utvärderas.

När du utvärderar principer med hjälp av datauppsättningsfält bör du tänka på följande:

* **Fältnamn är skiftlägeskänsliga**: När du anger fält måste de skrivas exakt som de visas i datauppsättningen (till exempel `firstName` vs `firstname`).
* **Arv av datauppsättningsetikett**: Enskilda fält i en datauppsättning ärver alla etiketter som har tillämpats på datauppsättningsnivån. Om dina principutvärderingar inte returneras som förväntat ska du kontrollera om det finns etiketter som kan ha ärvts från datauppsättningsnivån ned till fält, utöver de som tillämpas på fältnivån.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på marknadsföringsåtgärden som ska testas mot en delmängd av datamängdsfält. Du kan hämta en lista över tillgängliga marknadsföringsåtgärder genom att skapa en [GET-begäran till slutpunkten för marknadsföringsåtgärder](./marketing-actions.md#list). |

**Begäran**

Följande förfrågan testar marknadsföringsåtgärden `crossSiteTargeting` på en specifik uppsättning fält som tillhör tre datamängder. Nyttolasten liknar [utvärderingsbegäran som endast innehåller datauppsättningar](#datasets), lägger till specifika fält för varje datauppsättning att samla in etiketter från.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `entityType` | Typen av enhet vars ID anges i jämställda `entityId` -egenskap. För närvarande är det enda godkända värdet `dataSet`. |
| `entityId` | ID:t för en datauppsättning vars fält ska utvärderas mot marknadsföringsåtgärden. En lista över datauppsättningar och deras motsvarande ID:n kan hämtas genom att en GET-begäran görs till `/dataSets` slutpunkt i [!DNL Catalog Service] API. Se guiden på [lista [!DNL Catalog] objekt](../../catalog/api/list-objects.md) för mer information. |
| `entityMeta.fields` | En array med sökvägar till specifika fält i datasetets schema, som tillhandahålls i form av JSON-pekarsträngar. Se avsnittet om [JSON-pekare](../../landing/api-fundamentals.md#json-pointer) i guiden om grundläggande API-funktioner om du vill ha mer information om den godkända syntaxen för de här strängarna. |

**Svar**

Ett lyckat svar innehåller `violatedPolicies` -matris, som innehåller information om de principer som överträtts till följd av att marknadsföringsåtgärden utfördes mot de angivna datauppsättningsfälten. Om inga policyer överträds `violatedPolicies` matrisen kommer att vara tom.

Jämföra exempelsvaret nedan med [svar som endast innehåller datauppsättningar](#datasets)Observera att listan med samlade etiketter är kortare. The `discoveredLabels` för varje datauppsättning har också reducerats, eftersom de endast innehåller de fält som anges i begärandetexten. Dessutom bröt den tidigare principen `Targeting Ads or Content` kräver båda `C4 AND C6` etiketter som ska visas och som därför inte längre bryts enligt de tomma `violatedPolicies` array.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Utvärdera policyer i grupp {#bulk}

The `/bulk-eval` kan du köra flera utvärderingsjobb i ett enda API-anrop.

**API-format**

```http
POST /bulk-eval
```

**Begäran**

Nyttolasten för en grupputvärderingsbegäran ska vara en array med objekt, en för varje utvärderingsjobb som ska utföras. För jobb som utvärderas baserat på datamängder och fält kan `entityList` matris måste anges. För jobb som utvärderas baserat på dataanvändningsetiketter är en `labels` matris måste anges.

>[!WARNING]
>
>Om ett utvärderingsjobb i listan innehåller båda `entityList` och `labels` -matrisen resulterar ett fel. Om du vill utvärdera samma marknadsföringsåtgärd baserat på både datauppsättningar och etiketter måste du inkludera separata utvärderingsjobb för den marknadsföringsåtgärden.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `evalRef` | URI:n för marknadsföringsåtgärden som ska testas mot etiketter eller datauppsättningar för policyöverträdelser. |
| `includeDraft` | Som standard deltar endast aktiverade profiler i utvärderingen. If `includeDraft` är inställd på `true`, profiler som `DRAFT` kommer också att delta. |
| `labels` | En matris med dataanvändningsetiketter för att testa marknadsföringsåtgärden mot.<br><br>**VIKTIGT**: När den här egenskapen används, `entityList` får INTE ingå i samma objekt. Om du vill utvärdera samma marknadsföringsåtgärd med hjälp av datauppsättningar och/eller fält måste du inkludera ett separat objekt i nyttolasten som innehåller en `entityList` array. |
| `entityList` | En array med datauppsättningar och (eventuellt) specifika fält i dessa datauppsättningar för att testa marknadsföringsåtgärden mot.<br><br>**VIKTIGT**: När den här egenskapen används, `labels` får INTE ingå i samma objekt. Om du vill utvärdera samma marknadsföringsåtgärd med hjälp av specifika etiketter för dataanvändning måste du inkludera ett separat objekt i nyttolasten som innehåller en `labels` array. |
| `entityType` | Den typ av enhet som marknadsföringsåtgärden ska testas mot. För närvarande, endast `dataSet` stöds. |
| `entityId` | ID:t för en datauppsättning som marknadsföringsåtgärden ska testas mot. |
| `entityMeta.fields` | (Valfritt) En lista med specifika fält i datauppsättningen som marknadsföringsåtgärden ska testas mot. |

**Svar**

Ett lyckat svar returnerar en array med utvärderingsresultat, ett för varje principutvärderingsjobb som skickats i begäran.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{ORG_ID}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Policyutvärdering för [!DNL Real-Time Customer Profile]

The [!DNL Policy Service] API kan också användas för att kontrollera om det finns policyöverträdelser där [!DNL Real-Time Customer Profile] segment. Se självstudiekursen om [se till att dataanvändningen efterlevs för målgruppssegment](../../segmentation/tutorials/governance.md) för mer information.
