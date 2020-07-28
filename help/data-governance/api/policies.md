---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Profiler
topic: developer guide
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---


# Profiler

Dataanvändningspolicyer är regler som organisationen antar som beskriver den typ av marknadsföringsåtgärder som ni tillåts eller begränsas från att utföra på data inom [!DNL Experience Platform].

Slutpunkten används `/policies` för alla API-anrop som rör visning, skapande, uppdatering eller borttagning av dataanvändningsprinciper.

## Visa alla principer

Om du vill visa en lista med principer kan du göra en GET-förfrågan till `/policies/core` eller `/policies/custom` som returnerar alla profiler för den angivna behållaren.

**API-format**

```http
GET /policies/core
GET /policies/custom
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller ett antal som visar det totala antalet principer i den angivna behållaren samt information om varje princip inklusive dess `id`. Fältet används `id` för att utföra sökförfrågningar för att visa specifika principer samt för att utföra uppdaterings- och borttagningsåtgärder.

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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550701472910,
            "updatedClient": "string",
            "updatedUser": "string",
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714340335,
            "updatedClient": "string",
            "updatedUser": "string",
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

## Söka efter en princip

Varje princip innehåller ett `id` fält som kan användas för att begära information om en viss princip. Om en `id` princips status är okänd kan den hittas med listbegäran (GET) för att lista alla principer i en viss behållare (`core` eller `custom`), vilket visades i föregående steg.

**API-format**

```http
GET /policies/core/{id}
GET /policies/custom/{id}
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller detaljerad information om policyn, inklusive nyckelfält som `id` (det här fältet ska matcha det `id` som skickats i begäran), `name`, `status`och `description`, samt en referenslänk till den marknadsföringsåtgärd som policyn baseras på (`marketingActionRefs`).

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
    "created": 1550691551888,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Skapa en profil {#create-policy}

För att skapa en policy måste en marknadsföringsåtgärd ingå med ett uttryck för DULE-etiketterna som förbjuder den marknadsföringsåtgärden. Principdefinitionerna måste innehålla en `deny` egenskap, som är ett booleskt uttryck som anger förekomsten av DULE-etiketter.

Det här uttrycket kallas ett `PolicyExpression` och är ett objekt som innehåller _antingen_ en etikett _eller_ en operator och operander, men inte båda. I sin tur är varje operand också ett `PolicyExpression` objekt. En policy för export av data till en tredje part kan till exempel vara förbjuden om det finns `C1 OR (C3 AND C7)` etiketter. Detta uttryck skulle anges som:

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

**API-format**

```http
POST /policies/custom
```

**Begäran**

```SHELL
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
          "../marketingActions/custom/exportToThirdParty"
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

**Svar**

Om det skapas får du en HTTP-status 201 (Skapad) och svarstexten innehåller information om den nya principen, inklusive dess `id`. Värdet är skrivskyddat och tilldelas automatiskt när profilen skapas.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550691551888,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Uppdatera en profil

Du kanske måste uppdatera en dataanvändningsprincip när den har skapats. Detta görs genom en PUT-begäran till policyn `id` med en nyttolast som innehåller den uppdaterade formen av policyn i sin helhet. Med andra ord är begäran från PUT i stort sett en _omskrivning_ av policyn, och därför måste den innehålla all nödvändig information som visas i exemplet nedan.

**API-format**

```http
PUT /policies/custom/{id}
```

**Begäran**

I det här exemplet har villkoren för att exportera data till en tredje part ändrats, och nu måste du använda den princip som du skapade för att neka den här marknadsföringsåtgärden om det finns `C1 AND (C3 OR C7)` dataetiketter. Du använder följande anrop för att uppdatera den befintliga profilen.

```SHELL
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
            {
              "operator": "OR",
              "operands": [
                {"label": "C3"},
                {"label": "C7"}
              ]
            }
          ]
        }
      }'
```

**Svar**

En slutförd uppdateringsbegäran returnerar HTTP-status 200 (OK) och svarstexten visar den uppdaterade principen. Den `id` ska matcha den `id` som skickas i begäran.

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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550701472910,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Uppdatera en del av en princip

En viss del av en policy kan uppdateras på PATCH-begäran. Till skillnad från PUT som _skriver_ om principen begär PATCH endast att den sökväg som angetts i begärandetexten ska uppdateras. Detta är särskilt användbart när du vill aktivera eller inaktivera en profil, eftersom du bara behöver skicka den specifika sökvägen som du vill uppdatera (`/status`) och dess värde (`ENABLE` eller `DISABLE`).

API:t har för närvarande stöd för åtgärderna&quot;add&quot;,&quot;replace&quot; och&quot;remove&quot; PATCH och gör att du kan kombinera flera uppdateringar till ett enda anrop genom att lägga till var och en som ett objekt i arrayen, vilket visas i följande exempel. [!DNL Policy Service]

**API-format**

```http
PATCH /policies/custom/{id}
```

**Begäran**

I det här exemplet använder vi åtgärden&quot;replace&quot; för att ändra principstatusen från&quot;DRAFT&quot; till&quot;ENABLED&quot; och för att uppdatera beskrivningsfältet med en ny beskrivning. Vi kan också ha uppdaterat beskrivningsfältet genom att använda åtgärden &quot;ta bort&quot; för att ta bort principbeskrivningen och sedan använda åtgärden &quot;lägg till&quot; för att lägga till en ny gång, som i följande exempel:

```SHELL
[
    {
        "op": "remove",
        "path": "/description"
    },
    {
        "op": "add",
        "path": "/description",
        "value": "New policy description."
    }
]
```

När du skickar flera PATCH-åtgärder i en enda begäran måste du komma ihåg att de kommer att behandlas i den ordning som de visas i arrayen, så se till att du skickar förfrågningarna i rätt ordning där det behövs.

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

En slutförd uppdateringsbegäran returnerar HTTP-status 200 (OK) och svarstexten visar den uppdaterade principen (&quot;status&quot; är nu &quot;ENABLED&quot; och &quot;description&quot; har ändrats). Principen `id` ska matcha den `id` som skickats i begäran.


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
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550712163182,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6dacdf685a4913dc48937c"
        }
    },
    "id": "5c6dacdf685a4913dc48937c"
}
```

## Ta bort en profil

Om du behöver ta bort en profil som du har skapat kan du göra det genom att skicka en DELETE-begäran till den `id` profil som du vill ta bort. Det är bäst att först utföra en sökning (GET)-begäran för att visa principen och bekräfta att det är rätt princip som du vill ta bort. **Policyer kan inte återställas när de har tagits bort.**

**API-format**

```http
DELETE /policies/custom/{id}
```

**Begäran**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb56eb60ca13dbf8b9a8 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Om principen har tagits bort, kommer svarstexten att vara tom med HTTP-status 200 (OK).

Du kan bekräfta borttagningen genom att försöka söka efter (GET) profilen igen. Du bör få ett HTTP-status 404 (Hittades inte) tillsammans med felmeddelandet &quot;Hittades inte&quot; eftersom principen har tagits bort.
