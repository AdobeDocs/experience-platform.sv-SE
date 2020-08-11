---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Profiler
topic: developer guide
translation-type: tm+mt
source-git-commit: 7bc7050d64727f09d3a13d803d532a9a3ba5d1a7
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 0%

---


# Profilslutpunkt

Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data inom [!DNL Experience Platform]. Med slutpunkten i `/policies`[!DNL Policy Service API] kan ni programmässigt hantera dataanvändningsprinciper för organisationen.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Innan du fortsätter bör du läsa [Komma igång-guiden](getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API i det här dokumentet samt viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform] -API.

## Hämta en lista med profiler {#list}

Du kan visa alla `core` - eller `custom` -profiler genom att göra en GET-förfrågan till `/policies/core` respektive `/policies/custom`.

**API-format**

```http
GET /policies/core
GET /policies/custom
```

**Begäran**

Följande begäran hämtar en lista med anpassade principer som definierats av din organisation.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar innehåller en `children` array med information om alla hämtade principer, inklusive deras `id` värden. Du kan använda fältet `id` för en viss princip för att utföra [sökning](#lookup), [uppdatering](#update)och [borttagning](#delete) av begäranden för den principen.

```JSON
{
    "_page": {
        "start": "5c6dacdf685a4913dc48937c",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/policies/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "Export Data to Third Party",
            "status": "DRAFT",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
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
            "created": 1550691551888,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550701472910,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
                }
            },
            "id": "5c6dacdf685a4913dc48937c"
        },
        {
            "name": "Combine Data",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
            ],
            "description": "Data that meets these conditions cannot be combined.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C3"
                    },
                    {
                        "label": "I1"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1550714340335,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
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

| Egenskap | Beskrivning |
| --- | --- |
| `_page.count` | Det totala antalet principer som har hämtats. |
| `name` | Visningsnamnet för en princip. |
| `status` | Aktuell status för en princip. Det finns tre möjliga statusar: `DRAFT`, `ENABLED`eller `DISABLED`. Som standard deltar endast `ENABLED` policyer i utvärderingen. Mer information finns i översikten över [policyutvärdering](../enforcement/overview.md) . |
| `marketingActionRefs` | En array som listar URI:erna för alla tillämpliga marknadsföringsåtgärder för en princip. |
| `description` | En valfri beskrivning som ger ytterligare kontext till principens användningsfall. |
| `deny` | Ett objekt som beskriver de specifika dataanvändningsetiketter som en princips associerade marknadsföringsåtgärd är begränsad från att utföras på. Mer information om den här egenskapen finns i avsnittet [Skapa en profil](#create-policy) . |

## Söka efter en princip {#look-up}

Du kan söka efter en viss princip genom att ta med den principens `id` egenskap i sökvägen för en GET-begäran.

**API-format**

```http
GET /policies/core/{POLICY_ID}
GET /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | Vilken policy `id` du vill söka efter. |

**Begäran**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om principen.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550714340335,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Principens visningsnamn. |
| `status` | Principens aktuella status. Det finns tre möjliga statusar: `DRAFT`, `ENABLED`eller `DISABLED`. Som standard deltar endast `ENABLED` policyer i utvärderingen. Mer information finns i översikten över [policyutvärdering](../enforcement/overview.md) . |
| `marketingActionRefs` | En array som listar URI:erna för alla tillämpliga marknadsföringsåtgärder för principen. |
| `description` | En valfri beskrivning som ger ytterligare kontext till principens användningsfall. |
| `deny` | Ett objekt som beskriver de specifika dataanvändningsetiketter som principens associerade marknadsföringsåtgärd är begränsad från att utföras på. Mer information om den här egenskapen finns i avsnittet [Skapa en profil](#create-policy) . |

## Skapa en anpassad profil {#create-policy}

I API:t [!DNL Policy Service] definieras en princip av följande:

* En referens till en viss marknadsföringsåtgärd
* Ett uttryck som beskriver dataanvändningsetiketterna som marknadsföringsåtgärden är begränsad från att utföras mot

För att uppfylla det senare kravet måste principdefinitionerna innehålla ett booleskt uttryck om förekomsten av dataanvändningsetiketter. Det här uttrycket kallas ett **principuttryck**.

Policyuttryck tillhandahålls i form av en `deny` egenskap i varje principdefinition. Ett exempel på ett enkelt `deny` objekt som bara kontrollerar om det finns en enda etikett ser ut så här:

```json
"deny": {
    "label": "C1"
}
```

Många principer anger dock mer komplexa villkor för förekomsten av dataanvändningsetiketter. Om du vill ha stöd för dessa användningsfall kan du även inkludera booleska åtgärder som beskriver dina policyuttryck. Principuttrycksobjektet måste innehålla _antingen_ en etikett _eller_ en operator och operander, men inte båda. I sin tur är varje operand också ett principuttrycksobjekt.

För att definiera en princip som förhindrar att en marknadsföringsåtgärd utförs på data där det finns `C1 OR (C3 AND C7)` etiketter, skulle principens `deny` egenskap anges som:

```JSON
"deny": {
  "operator": "OR",
  "operands": [
    {"label": "C1"},
    {
      "operator": "AND",
      "operands": [
        {"label": "C3"},
        {"label": "C7"}
      ]
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `operator` | Anger den villkorliga relationen mellan etiketterna i `operands` syskonarrayen. Godkända värden är: <ul><li>`OR`: Uttrycket tolkas som true om någon av etiketterna i `operands` arrayen finns.</li><li>`AND`: Uttrycket tolkas bara till true om alla etiketter i `operands` arrayen finns.</li></ul> |
| `operands` | En array med objekt där varje objekt representerar antingen en enda etikett eller ytterligare ett par `operator` och `operands` egenskaper. Förekomsten av etiketter och/eller åtgärder i en `operands` array tolkas som true eller false baserat på värdet för dess `operator` jämställda egenskap. |
| `label` | Namnet på en enskild dataanvändningsetikett som gäller för principen. |

Du kan skapa en ny anpassad princip genom att göra en begäran om POST till `/policies/custom` slutpunkten.

**API-format**

```http
POST /policies/custom
```

**Begäran**

Följande begäran skapar en ny princip som begränsar marknadsföringsåtgärden `exportToThirdParty` från att utföras på data som innehåller etiketter `C1 OR (C3 AND C7)`.

```sh
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "OR",
          "operands": [
            {"label": "C1"},
            {
              "operator": "AND",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Principens visningsnamn. |
| `status` | Principens aktuella status. Det finns tre möjliga statusar: `DRAFT`, `ENABLED`eller `DISABLED`. Som standard deltar endast `ENABLED` policyer i utvärderingen. Mer information finns i översikten över [policyutvärdering](../enforcement/overview.md) . |
| `marketingActionRefs` | En array som listar URI:erna för alla tillämpliga marknadsföringsåtgärder för principen. URI:n för en marknadsföringsåtgärd anges `_links.self.href` i svaret för att [hitta en marknadsföringsåtgärd](./marketing-actions.md#look-up). |
| `description` | En valfri beskrivning som ger ytterligare kontext till principens användningsfall. |
| `deny` | Principuttrycket som beskriver de specifika dataanvändningsetiketter som principens associerade marknadsföringsåtgärd är begränsad från att utföras på. |

**Svar**

Ett lyckat svar returnerar information om den nya principen, inklusive dess `id`. Värdet är skrivskyddat och tilldelas automatiskt när profilen skapas.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
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
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550691551888,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Uppdatera en anpassad princip {#update}

>[!IMPORTANT]
>
>Du kan bara uppdatera anpassade profiler. Om du vill aktivera eller inaktivera kärnprinciper läser du avsnittet om att [uppdatera listan över aktiverade kärnprinciper](#update-enabled-core).

Du kan uppdatera en befintlig anpassad princip genom att ange dess ID i sökvägen till en PUT-begäran med en nyttolast som innehåller den uppdaterade formen av profilen i sin helhet. Med andra ord skriver PUT i själva verket _om policyn_ .

>[!NOTE]
>
>Se avsnittet om hur du [uppdaterar en del av en anpassad profil](#patch) om du bara vill uppdatera ett eller flera fält för en profil, i stället för att skriva över den.

**API-format**

```http
PUT /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | Namnet `id` på profilen som du vill uppdatera. |

**Begäran**

I det här exemplet har villkoren för att exportera data till en tredje part ändrats, och nu måste du använda den princip som du skapade för att neka den här marknadsföringsåtgärden om det finns `C1 AND C5` dataetiketter.

Följande begäran uppdaterar den befintliga principen så att den inkluderar det nya principuttrycket. Observera att eftersom denna begäran i princip skriver om principen måste alla fält inkluderas i nyttolasten, även om vissa av deras värden inte uppdateras.

```sh
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Export Data to Third Party",
        "status": "DRAFT",
        "marketingActionRefs": [
          "../marketingActions/custom/exportToThirdParty"
        ],
        "description": "Conditions under which data cannot be exported to a third party",
        "deny": {
          "operator": "AND",
          "operands": [
            {"label": "C1"},
            {"label": "C5"}
          ]
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Principens visningsnamn. |
| `status` | Principens aktuella status. Det finns tre möjliga statusar: `DRAFT`, `ENABLED`eller `DISABLED`. Som standard deltar endast `ENABLED` policyer i utvärderingen. Mer information finns i översikten över [policyutvärdering](../enforcement/overview.md) . |
| `marketingActionRefs` | En array som listar URI:erna för alla tillämpliga marknadsföringsåtgärder för principen. URI:n för en marknadsföringsåtgärd anges `_links.self.href` i svaret för att [hitta en marknadsföringsåtgärd](./marketing-actions.md#look-up). |
| `description` | En valfri beskrivning som ger ytterligare kontext till principens användningsfall. |
| `deny` | Principuttrycket som beskriver de specifika dataanvändningsetiketter som principens associerade marknadsföringsåtgärd är begränsad från att utföras på. Mer information om den här egenskapen finns i avsnittet [Skapa en profil](#create-policy) . |

**Svar**

Ett godkänt svar returnerar information om den uppdaterade principen.

```JSON
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/core/exportToThirdParty"
    ],
    "description": "Conditions under which data cannot be exported to a third party",
    "deny": {
        "operator": "AND",
        "operands": [
            {
                "label": "C1"
            },
            {
                "label": "C5"
            }
        ]
    },
    "imsOrg": "{IMS_ORG}",
    "created": 1550691551888,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550701472910,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Uppdatera en del av en anpassad princip {#patch}

>[!IMPORTANT]
>
>Du kan bara uppdatera anpassade profiler. Om du vill aktivera eller inaktivera kärnprinciper läser du avsnittet om att [uppdatera listan över aktiverade kärnprinciper](#update-enabled-core).

En viss del av en policy kan uppdateras på PATCH-begäran. Till skillnad från PUT som skriver om principen begär PATCH endast att egenskaperna som anges i begärandetexten ska uppdateras. Detta är särskilt användbart när du vill aktivera eller inaktivera en profil, eftersom du bara behöver ange sökvägen till rätt egenskap (`/status`) och dess värde (`ENABLED` eller `DISABLED`).

>[!NOTE]
>
>Nyttolaster för PATCH-begäranden följer JSON-korrigeringsformatering. Mer information om godkänd syntax finns i [API-handboken](../../landing/api-fundamentals.md) .

API:t [!DNL Policy Service] stöder JSON-lagningsåtgärderna `add`, `remove`och `replace`gör att du kan kombinera flera uppdateringar till ett enda anrop, vilket visas i exemplet nedan.

**API-format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | Namnet `id` på den princip vars egenskaper du vill uppdatera. |

**Begäran**

Följande begäran använder två `replace` åtgärder för att ändra principstatus från `DRAFT` till `ENABLED`och för att uppdatera `description` fältet med en ny beskrivning.

>[!IMPORTANT]
>
>När du skickar flera PATCH-åtgärder i en enda begäran, bearbetas de i den ordning som de visas i arrayen. Se till att du skickar förfrågningarna i rätt ordning där det behövs.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' [
          {
            "op": "replace",
            "path": "/status",
            "value": "ENABLED"
          },
          {
            "op": "replace",
            "path": "/description",
            "value": "New policy description."
          }
        ]'
```

**Svar**

Ett godkänt svar returnerar information om den uppdaterade principen.


```JSON
{
    "name": "Export Data to Third Party",
    "status": "ENABLED",
    "marketingActionRefs": [
        "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
    ],
    "description": "New policy description.",
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
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1550712163182,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Ta bort en anpassad princip {#delete}

Du kan ta bort en anpassad princip genom att ta med den `id` i sökvägen för en DELETE-begäran.

>[!WARNING]
>
>Policyer kan inte återställas när de har tagits bort. Det är bäst att [först utföra en sökning (GET)-begäran](#lookup) för att visa principen och bekräfta att det är rätt princip som du vill ta bort.

**API-format**

```http
DELETE /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | ID för profilen som du vill ta bort. |

**Begäran**

```sh
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med en tom brödtext.

Du kan bekräfta borttagningen genom att försöka söka efter (GET) profilen igen. Du bör få ett HTTP 404-fel (Hittades inte) om principen har tagits bort.

## Hämta en lista över aktiverade kärnprinciper {#list-enabled-core}

Som standard deltar endast aktiverade dataanvändningsprinciper i utvärderingen. Du kan hämta en lista över kärnprinciper som för närvarande är aktiverade av din organisation genom att göra en GET-förfrågan till `/enabledCorePolicies` slutpunkten.

**API-format**

```http
GET /enabledCorePolicies
```

**Begäran**

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar listan med aktiverade kärnprinciper under en `policyIds` array.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0003",
    "corepolicy_0004",
    "corepolicy_0005",
    "corepolicy_0006",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Uppdatera listan över aktiverade kärnprinciper {#update-enabled-core}

Som standard deltar endast aktiverade dataanvändningsprinciper i utvärderingen. Genom att göra en PUT-begäran till `/enabledCorePolicies` slutpunkten kan du uppdatera listan över aktiverade kärnprinciper för din organisation med ett enda samtal.

>[!NOTE]
>
>Endast kärnprinciper kan aktiveras eller inaktiveras av den här slutpunkten. Information om hur du aktiverar eller inaktiverar anpassade profiler finns i avsnittet [Uppdatera en del av en profil](#patch).

**API-format**

```http
PUT /enabledCorePolicies
```

**Begäran**

Följande begäran uppdaterar listan med aktiverade kärnprinciper baserat på ID:n som anges i nyttolasten.

```sh
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/enabledCorePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "policyIds": [
          "corepolicy_0001",
          "corepolicy_0002",
          "corepolicy_0007",
          "corepolicy_0008"
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `policyIds` | En lista över princip-ID:n som ska aktiveras. Alla viktiga policyer som inte ingår anges till `DISABLED` status och kommer inte att delta i utvärderingen. |

**Svar**

Ett lyckat svar returnerar den uppdaterade listan över aktiverade kärnprinciper under en `policyIds` array.

```json
{
  "policyIds": [
    "corepolicy_0001",
    "corepolicy_0002",
    "corepolicy_0007",
    "corepolicy_0008"
  ],
  "imsOrg": "{IMS_ORG}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1595876052649,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/enabledCorePolicies"
    }
  }
}
```

## Nästa steg

När du har definierat nya eller uppdaterade principer kan du använda API:t för att testa marknadsföringsåtgärder mot specifika etiketter eller datauppsättningar och se om dina policyer ger upphov till överträdelser som förväntat. [!DNL Policy Service] Mer information finns i guiden om [policyutvärderingsslutpunkterna](./evaluation.md) .