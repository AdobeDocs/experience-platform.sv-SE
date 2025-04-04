---
keywords: Experience Platform;hem;populära ämnen;Politiska frågor;Automatisk tillsyn;API-baserad tillämpning;datastyrning;testning
solution: Experience Platform
title: Tvinga dataanvändningsprinciper med hjälp av API:t för principtjänsten
type: Tutorial
description: När du har skapat dataanvändningsetiketter för dina data, och har skapat användningsprinciper för marknadsföringsåtgärder mot dessa etiketter, kan du använda principtjänstens API för att utvärdera om en marknadsföringsåtgärd som utförs på en datauppsättning eller en godtycklig grupp av etiketter utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# Använd dataanvändningsprinciper med API:t [!DNL Policy Service]

När du har skapat etiketter för dataanvändning för dina data och har skapat användarprofiler för marknadsföringsåtgärder mot dessa etiketter, kan du använda [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) för att utvärdera om en marknadsföringsåtgärd som har utförts på en datauppsättning eller en godtycklig grupp av etiketter utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.

>[!NOTE]
>
>Som standard kan endast principer med statusen `ENABLED` delta i utvärderingen. Om du vill tillåta `DRAFT`-principer att delta i utvärderingen måste du inkludera frågeparametern `includeDraft=true` i sökvägen till begäran.

Det här dokumentet innehåller steg om hur du använder API:t [!DNL Policy Service] för att söka efter policyöverträdelser i olika scenarier.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande viktiga begrepp som används i att implementera dataanvändningspolicyer:

* [Datastyrning](../home.md): Ramverket som [!DNL Experience Platform] använder för att framtvinga efterlevnad av dataanvändning.
   * [Dataanvändningsetiketter](../labels/overview.md): Dataanvändningsetiketter används för datauppsättningar (och/eller enskilda fält inom dessa datauppsättningar), vilket anger begränsningar för hur data kan användas.
   * [Dataanvändningsprinciper](../policies/overview.md): Dataanvändningsprinciper är regler som beskriver vilken typ av marknadsföringsåtgärder som tillåts eller begränsas för vissa uppsättningar dataanvändningsetiketter.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till [!DNL Policy Service]-API:t, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Utvärdera med hjälp av etiketter och en marknadsföringsåtgärd

Du kan utvärdera en policy genom att testa en marknadsföringsåtgärd mot en uppsättning dataanvändningsetiketter som skulle finnas i en datauppsättning. Detta görs med frågeparametern `duleLabels`, där etiketter anges som en kommaavgränsad lista med värden, vilket visas i exemplet nedan.

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

Följande begäran testar marknadsföringsåtgärden `exportToThirdParty` mot etiketterna `C1` och `C3`. Eftersom dataanvändningsprincipen som du skapade tidigare i den här självstudien definierar etiketten `C1` som ett av `deny` -villkoren i dess principuttryck, bör marknadsföringsåtgärden utlösa en principöverträdelse.

>[!NOTE]
>
>Dataanvändningsetiketter är skiftlägeskänsliga. Policyöverträdelser inträffar endast när etiketterna som definieras i deras policyuttryck matchar exakt. I det här exemplet skulle en `C1`-etikett utlösa en överträdelse, men en `c1`-etikett skulle inte göra det.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, användningsetiketterna som den testades mot och en lista över profiler som överträds som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen Exportera data till tredje part i arrayen `violatedPolicies`, vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

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
| `violatedPolicies` | En matris med en lista över principer som har överträtts genom att marknadsföringsåtgärden (anges i `marketingActionRef`) testas mot den angivna `duleLabels`. |

## Utvärdera med datauppsättningar

Du kan utvärdera en dataanvändningsprincip genom att testa en marknadsföringsåtgärd mot en eller flera datauppsättningar från vilka etiketter kan samlas in. Detta görs genom att en POST-begäran görs till `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` och datauppsättnings-ID:n tillhandahålls i begärandetexten, vilket visas i exemplet nedan.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som är associerad med policyn som du utvärderar. |

**Begäran**

Följande begäran testar marknadsföringsåtgärden `exportToThirdParty` mot tre olika datamängder. Datamängderna refereras av typen och ID i en array som tillhandahålls i nyttolasten.

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
| `entityType` | Varje objekt i nyttolastarrayen måste ange vilken typ av enhet som definieras. I det här fallet är värdet alltid&quot;dataSet&quot;. |
| `entityId` | Varje objekt i nyttolastarrayen måste ange det unika ID:t för en datamängd. |
| `entityMeta.fields` | (Valfritt) En matris med [JSON-pekarsträngar](../../landing/api-fundamentals.md#json-pointer) som refererar till specifika fält i datasetens schema. Om den här arrayen inkluderas endast fälten i arrayen i utvärderingen. Schemafält som inte ingår i arrayen kommer inte att utvärderas.<br><br>Om det här fältet inte ingår inkluderas alla fält i datasetet i utvärderingen. |

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, de användningsetiketter som samlades in från de angivna datauppsättningarna och en lista över principer som överträtts som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen Exportera data till tredje part i arrayen `violatedPolicies`, vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

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
| `violatedPolicies` | En matris med en lista över principer som har överträtts genom att marknadsföringsåtgärden (anges i `marketingActionRef`) testas mot den angivna `duleLabels`. |

## Nästa steg

Genom att läsa det här dokumentet har du sökt efter policyöverträdelser när du utför en marknadsföringsåtgärd på en datauppsättning eller en uppsättning dataanvändningsetiketter. Med hjälp av data som returneras i API-svar kan du konfigurera protokoll i ditt upplevelseprogram så att regelöverträdelser verkställs korrekt när de inträffar.

Mer information om hur Experience Platform automatiskt tillämpar skyddsprofiler för aktiverade segment finns i handboken om [automatisk tillämpning](./auto-enforcement.md).
