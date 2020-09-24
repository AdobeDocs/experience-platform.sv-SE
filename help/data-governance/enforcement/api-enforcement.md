---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance;testing
solution: Experience Platform
title: Använd principer för dataanvändning med hjälp av API:t för principtjänsten
topic: enforcement
type: Tutorial
description: När du har skapat dataanvändningsetiketter för dina data, och har skapat användningsprinciper för marknadsföringsåtgärder mot dessa etiketter, kan du använda principtjänstens API för att utvärdera om en marknadsföringsåtgärd som utförs på en datauppsättning eller en godtycklig grupp av etiketter utgör en policyöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---


# Använd principer för dataanvändning med [!DNL Policy Service] API

När du har skapat dataanvändningsetiketter för dina data och skapat användarprofiler för marknadsföringsåtgärder mot dessa etiketter kan du använda [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) för att utvärdera om en marknadsföringsåtgärd som har utförts på en datauppsättning eller en godtycklig grupp av etiketter utgör en principöverträdelse. Du kan sedan konfigurera egna interna protokoll för att hantera policyöverträdelser baserat på API-svaret.

>[!NOTE]
>
>Som standard kan endast profiler vars status är inställd på `ENABLED` delta i utvärderingen. Om du vill tillåta `DRAFT` profiler att delta i utvärderingen måste du ta med frågeparametern `includeDraft=true` i sökvägen till begäran.

Det här dokumentet innehåller steg om hur du använder API:t för att söka efter policyöverträdelser i olika scenarier. [!DNL Policy Service]

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande viktiga begrepp som används i att implementera dataanvändningspolicyer:

* [Datastyrning](../home.md): Ramverket som [!DNL Platform] genomdriver efterlevnad av dataanvändning.
   * [Dataanvändningsetiketter](../labels/overview.md): Dataanvändningsetiketter används för datauppsättningar (och/eller enskilda fält inom dessa datauppsättningar), vilket anger begränsningar för hur data kan användas.
   * [Dataanvändningsprinciper](../policies/overview.md): Dataanvändningsprinciper är regler som beskriver den typ av marknadsföringsåtgärder som är tillåtna eller begränsade för vissa uppsättningar av dataanvändningsetiketter.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till [!DNL Policy Service] API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Utvärdera med hjälp av etiketter och en marknadsföringsåtgärd

Du kan utvärdera en policy genom att testa en marknadsföringsåtgärd mot en uppsättning dataanvändningsetiketter som skulle finnas i en datauppsättning. Detta görs med frågeparametern, där etiketter anges som en kommaavgränsad lista med värden, vilket visas i exemplet nedan. `duleLabels`

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

Följande begäran testar marknadsföringsåtgärden mot etiketter `exportToThirdParty` och `C1` `C3`. Eftersom den dataanvändningsprincip som du skapade tidigare i den här självstudiekursen definierar `C1` etiketten som ett av `deny` villkoren i dess policyuttryck, bör marknadsföringsåtgärden utlösa en principöverträdelse.

>[!NOTE]
>
>Dataanvändningsetiketter är skiftlägeskänsliga. Policyöverträdelser inträffar endast när etiketterna som definieras i deras policyuttryck matchar exakt. I det här exemplet skulle en `C1` etikett utlösa en överträdelse, medan en `c1` etikett inte skulle göra det.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, användningsetiketterna som den testades mot och en lista över profiler som överträds som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen&quot;Exportera data till tredje part&quot; i `violatedPolicies` arrayen, vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Du kan utvärdera en dataanvändningsprincip genom att testa en marknadsföringsåtgärd mot en eller flera datauppsättningar från vilka etiketter kan samlas in. Detta görs genom att en POST begär `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` och tillhandahåller datauppsättnings-ID i begärandetexten, vilket visas i exemplet nedan.

**API-format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som är associerad med policyn som du utvärderar. |

**Begäran**

Följande begäran testar marknadsföringsåtgärden mot tre olika datauppsättningar `exportToThirdParty` . Datamängderna refereras av typen och ID i en array som tillhandahålls i nyttolasten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `entityType` | Varje objekt i nyttolastarrayen måste ange vilken typ av enhet som definieras. I det här fallet kommer värdet alltid att vara &quot;dataSet&quot;. |
| `entityId` | Varje objekt i nyttolastarrayen måste ange ett unikt ID för en datamängd. |

**Svar**

Ett lyckat svar returnerar URL:en för marknadsföringsåtgärden, de användningsetiketter som samlades in från de angivna datauppsättningarna och en lista över principer som överträtts som ett resultat av att åtgärden testades mot dessa etiketter. I det här exemplet visas principen&quot;Exportera data till tredje part&quot; i `violatedPolicies` arrayen, vilket anger att marknadsföringsåtgärden utlöste den förväntade principöverträdelsen.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Anvisningar om hur du tillämpar dataanvändningspolicyer för målgruppssegment i [!DNL Real-time Customer Profile]finns i följande [självstudiekurs](../../segmentation/tutorials/governance.md).