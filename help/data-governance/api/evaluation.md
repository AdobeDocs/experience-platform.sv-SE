---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Profiler
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# Politisk utvärdering

När marknadsföringsåtgärder har skapats och principer har definierats, kan du använda API:t för att utvärdera om några profiler överträds av vissa åtgärder. [!DNL Policy Service] De returnerade begränsningarna har formen av en uppsättning principer som skulle överträdas om marknadsföringsåtgärden utförs på de angivna data som innehåller dataanvändningsetiketter.

Som standard deltar **bara profiler vars status är inställd på&quot;ENABLED&quot; i utvärderingen**, men du kan använda frågeparametern `?includeDraft=true` för att inkludera&quot;UTKAST&quot;-principer i utvärderingen.

Begäran om utvärdering kan göras på ett av tre sätt:

1. Om man utgår från en uppsättning dataanvändningsetiketter och en marknadsföringsåtgärd, bryter åtgärden mot några policyer?
1. Om man utgår från en eller flera datauppsättningar och en marknadsföringsåtgärd, bryter åtgärden mot några policyer?
1. Om en eller flera datauppsättningar och en deluppsättning av ett eller flera fält i var och en av dessa datauppsättningar anges, bryter åtgärden mot några policyer?

## Utvärdera policyer med hjälp av dataanvändningsetiketter och en marknadsföringsåtgärd

Utvärderingen av policyöverträdelser baserat på förekomsten av dataanvändningsetiketter kräver att du anger den uppsättning etiketter som skulle finnas på data under begäran. Detta görs med hjälp av frågeparametrar, där dataanvändningsetiketter anges som en kommaavgränsad lista med värden, vilket visas i följande exempel.

**API-format**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Begäran**

Exemplet nedan utvärderar en marknadsföringsåtgärd mot etiketterna C1 och C3. Tänk på följande när du utvärderar profiler med hjälp av dataanvändningsetiketter:
* **Dataanvändningsetiketter är skiftlägeskänsliga.** Begäran som visas ovan returnerar en felaktig princip, men samma begäran görs med gemener (t.ex. etiketter). `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) inte.
* **Var medveten om operatorerna`AND`och`OR`operatorerna i dina policyuttryck.** I det här exemplet skulle marknadsföringsåtgärden inte ha brutit mot denna policy om etiketten (`C1` eller `C3`) hade funnits ensam i begäran. Det krävs båda etiketterna (`C1 AND C3`) för att returnera den felaktiga profilen. Se till att ni utvärderar policyer noggrant och definierar politiska uttryck med lika stor omsorg.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektet innehåller en `duleLabels` array som ska matcha de etiketter som skickats i begäran. Om den angivna marknadsföringsåtgärden mot dataanvändningsetiketterna bryter mot en princip, innehåller arrayen information om den eller de profiler som påverkas. `violatedPolicies` Om inga principer överträds visas `violatedPolicies` arrayen tom (`[]`).

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Utvärdera policyer med datauppsättningar och en marknadsföringsåtgärd

Du kan också utvärdera policyöverträdelser genom att ange ID:t för en eller flera datauppsättningar från vilka dataanvändningsetiketter kan samlas in. Detta görs genom att utföra en POST-begäran till antingen kärnan eller den anpassade `/constraints` slutpunkten för en marknadsföringsåtgärd och ange datauppsättnings-ID:n i begärandetexten, vilket visas nedan.

**API-format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Begäran**

Begärandetexten innehåller en array med ett objekt för varje datauppsättnings-ID. Eftersom du skickar en begärandetext visas&quot;Content-Type: application/json&quot; request header is required, as shown in the following example.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

**Svar**

Svarsobjektet innehåller en `duleLabels` array som innehåller en konsoliderad lista över alla etiketter som finns i de angivna datauppsättningarna. Den här listan innehåller datauppsättnings- och fältnivåetiketter för alla fält i datauppsättningen.

Svaret innehåller också en `discoveredLabels` array som innehåller objekt för varje datauppsättning och som visas `datasetLabels` uppdelat i etiketter på datamängd- och fältnivå. Varje etikett på fältnivå visar sökvägen till det specifika fältet med den etiketten.

Om den angivna marknadsföringsåtgärden bryter mot en princip som innehåller `duleLabels` data i datamängderna, innehåller `violatedPolicies` arrayen information om den eller de principer som påverkas. Om inga principer överträds visas `violatedPolicies` arrayen tom (`[]`).

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Utvärdera policyer med hjälp av datauppsättningar, fält och en marknadsföringsåtgärd

Förutom att ange ett eller flera datauppsättnings-ID:n kan en delmängd av fält från varje datauppsättning också anges, vilket anger att endast dataanvändningsetiketterna för dessa fält ska utvärderas. På samma sätt som POST-begäran som endast innehåller datauppsättningar lägger den här begäran till specifika fält för varje datauppsättning i begärandetexten.

När du utvärderar principer med hjälp av datauppsättningsfält bör du tänka på följande:

* **Fältnamn är skiftlägeskänsliga.** När du anger fält måste de skrivas exakt som de visas i datauppsättningen (till exempel `firstName` vs `firstname`).
* **Arv av datauppsättningsetikett.** dataanvändningsetiketter kan användas på flera nivåer och ärvs nedåt. Om dina principutvärderingar inte återställer det du trodde var möjligt ska du kontrollera de ärvda etiketterna från datauppsättningar ned till fält utöver de som tillämpas på fältnivån.

**API-format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Begäran**

Begärandetexten innehåller en array med ett objekt för varje datauppsättnings-ID och deluppsättningen med fält i den datauppsättningen som ska användas för utvärdering. Eftersom du skickar en begärandetext visas&quot;Content-Type: application/json&quot; request header is required, as shown in the following example.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Svar**

Svarsobjektet innehåller en `duleLabels` array som innehåller den konsoliderade listan med etiketter som finns i de angivna fälten. Kom ihåg att detta även omfattar datauppsättningsrubriker, eftersom de ärvs ned till fält.

Om en princip överträds genom att den angivna marknadsföringsåtgärden utförs på data i de angivna fälten, innehåller arrayen information om den (eller de) `violatedPolicies` principer som påverkas. Om inga principer överträds visas `violatedPolicies` arrayen tom (`[]`).

I svaret nedan ser du att listan med `duleLabels` `discoveredLabels` är kortare, liksom för varje datauppsättning eftersom den bara innehåller de fält som anges i begärandetexten. Du kommer också att märka att den tidigare oförenliga principen, &quot;Targeting Ads or Content&quot;, krävde båda `C4 AND C6` etiketterna, vilket innebär att den inte längre överträds och att `violatedPolicies` arrayen verkar vara tom.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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

## Policyutvärdering för [!DNL Real-time Customer Profile]

API:t kan också användas för att kontrollera om det finns policyöverträdelser som inbegriper användning av [!DNL Policy Service] [!DNL Real-time Customer Profile] segment. Mer information finns i självstudiekursen om hur ni [ser till att dataanvändningen efterlevs för målgruppssegment](../../segmentation/tutorials/governance.md) .