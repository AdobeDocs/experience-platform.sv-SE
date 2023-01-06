---
keywords: Experience Platform;hem;populära ämnen;Politiska frågor;Automatisk tillsyn;API-baserad tillämpning;datastyrning;testning
solution: Experience Platform
title: Tvinga dataanvändningsprinciper med hjälp av API:t för principtjänsten
type: Tutorial
description: När du har skapat dataanvändningsetiketter för dina data, och har skapat användningsprinciper för marknadsföringsåtgärder mot dessa etiketter, kan du använda principtjänstens API för att utvärdera om en marknadsföringsåtgärd som utförs på en datauppsättning eller en godtycklig grupp av etiketter utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# Använd dataanvändningsprinciper med [!DNL Policy Service] API

När du har skapat etiketter för dataanvändning för dina data, och har skapat profiler för marknadsföringsåtgärder mot dessa etiketter, kan du använda [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) utvärdera om en marknadsföringsåtgärd som utförs på en datauppsättning eller en godtycklig grupp av etiketter utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.

>[!NOTE]
>
>Som standard är det bara profiler vars status är inställd på `ENABLED` kan delta i utvärderingen. Tillåt `DRAFT` profiler för att delta i utvärderingen måste du inkludera frågeparametern `includeDraft=true` i sökvägen till begäran.

Det här dokumentet innehåller anvisningar om hur du använder [!DNL Policy Service] API för att söka efter policyöverträdelser i olika scenarier.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande viktiga begrepp som används i att implementera dataanvändningspolicyer:

* [Datastyrning](../home.md): Den ram som [!DNL Platform] regelefterlevnad för dataanvändning.
   * [Dataanvändningsetiketter](../labels/overview.md): Dataanvändningsetiketter används för datauppsättningar (och/eller enskilda fält inom dessa datauppsättningar), vilket anger begränsningar för hur data kan användas.
   * [Dataanvändningspolicyer](../policies/overview.md): Dataanvändningsprinciper är regler som beskriver den typ av marknadsföringsåtgärder som är tillåtna eller begränsade för vissa uppsättningar av dataanvändningsetiketter.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Innan du startar den här självstudiekursen bör du gå igenom [utvecklarhandbok](../api/getting-started.md) för viktig information som du behöver känna till för att kunna ringa [!DNL Policy Service] API, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Utvärdera med hjälp av etiketter och en marknadsföringsåtgärd

Du kan utvärdera en policy genom att testa en marknadsföringsåtgärd mot en uppsättning dataanvändningsetiketter som skulle finnas i en datauppsättning. Detta görs genom att `duleLabels` frågeparameter, där etiketter anges som en kommaavgränsad lista med värden, vilket visas i exemplet nedan.

**API-format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som är associerad med den dataanvändningsprincip som du utvärderar. |
| `{LABEL_1}` | En dataanvändningsetikett som testar marknadsföringsåtgärden mot. Minst en etikett måste anges. Om du anger flera etiketter måste de separeras med kommatecken. |

**Begäran**

Följande förfrågan testar `exportToThirdParty` marknadsföringsåtgärd mot etiketter `C1` och `C3`. Eftersom dataanvändningsprincipen som du skapade tidigare i den här självstudien definierar `C1` etikett som en av `deny` villkor i sitt policyuttryck bör marknadsföringsåtgärden utlösa en policyöverträdelse.

>[!NOTE]
>
>Dataanvändningsetiketter är skiftlägeskänsliga. Policyöverträdelser inträffar endast när etiketterna som definieras i deras policyuttryck matchar exakt. I det här exemplet `C1` label skulle utlösa en överträdelse, medan en `c1` etiketten skulle inte göra det.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, användningsetiketterna som den testades mot och en lista över profiler som överträds som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen &quot;Exportera data till tredje part&quot; i `violatedPolicies` , vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `violatedPolicies` | En array med en lista över principer som överträtts genom att marknadsföringsåtgärden testas (anges i `marketingActionRef`) mot den tillhandahållna `duleLabels`. |

## Utvärdera med datauppsättningar

Du kan utvärdera en dataanvändningsprincip genom att testa en marknadsföringsåtgärd mot en eller flera datauppsättningar från vilka etiketter kan samlas in. Detta gör du genom att göra en POST-förfrågan till `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` och tillhandahålla datauppsättnings-ID:n i begärandetexten, vilket visas i exemplet nedan.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som är associerad med policyn som du utvärderar. |

**Begäran**

Följande förfrågan testar `exportToThirdParty` marknadsföringsåtgärder mot tre olika datauppsättningar. Datamängderna refereras av typen och ID i en array som tillhandahålls i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `entityType` | Varje objekt i nyttolastarrayen måste ange vilken typ av enhet som definieras. I det här fallet kommer värdet alltid att vara &quot;dataSet&quot;. |
| `entityId` | Varje objekt i nyttolastarrayen måste ange ett unikt ID för en datamängd. |
| `entityMeta.fields` | (Valfritt) En array med [JSON-pekare](../../landing/api-fundamentals.md#json-pointer) strängar, referera till specifika fält i datasetens schema. Om den här arrayen inkluderas endast fälten i arrayen i utvärderingen. Schemafält som inte ingår i arrayen kommer inte att utvärderas.<br><br>Om det här fältet inte inkluderas inkluderas alla fält i datasetet i utvärderingen. |

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, de användningsetiketter som samlades in från de angivna datauppsättningarna och en lista över principer som överträtts som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen &quot;Exportera data till tredje part&quot; i `violatedPolicies` , vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `duleLabels` | En lista över dataanvändningsetiketter som har extraherats från datauppsättningarna som tillhandahålls i nyttolasten för begäran. |
| `discoveredLabels` | En lista över de datauppsättningar som tillhandahölls i nyttolasten för begäran, med information om de datauppsättningsnivårubriker och fältetiketter som hittades i varje. |
| `violatedPolicies` | En array med en lista över principer som överträtts genom att marknadsföringsåtgärden testas (anges i `marketingActionRef`) mot den tillhandahållna `duleLabels`. |

## Nästa steg

Genom att läsa det här dokumentet har du sökt efter policyöverträdelser när du utför en marknadsföringsåtgärd på en datauppsättning eller en uppsättning dataanvändningsetiketter. Med hjälp av data som returneras i API-svar kan du konfigurera protokoll i ditt upplevelseprogram så att regelöverträdelser verkställs korrekt när de inträffar.

Mer information om hur Platform automatiskt tillämpar regler för aktiverade segment finns i handboken om [automatisk tillämpning](./auto-enforcement.md).
