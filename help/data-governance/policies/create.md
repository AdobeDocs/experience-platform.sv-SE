---
keywords: Experience Platform;hem;populära ämnen;datastyrning;dataanvändningspolicy
solution: Experience Platform
title: Skapa en datahanteringsprincip i API:t
type: Tutorial
description: Lär dig hur du skapar en datahanteringsprincip med hjälp av API:t för principtjänsten.
exl-id: 8483f8a1-efe8-4ebb-b074-e0577e5a81a4
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 1%

---

# Skapa en datastyrningsprincip i API:t

The [API för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/) Med kan ni skapa och hantera datastyrningsprinciper för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa dataanvändningsetiketter.

I det här dokumentet finns en stegvis självstudiekurs för att skapa en styrningspolicy med [!DNL Policy Service] API.

>[!NOTE]
>
>Anvisningar om hur du skapar en åtkomstkontrollprincip finns i `/policies` slutpunktsguide för [API för åtkomstkontroll](../../access-control/abac/api/policies.md). Mer information om hur du skapar en policy för samtycke finns i [guide för användargränssnittet](./user-guide.md#consent-policy).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande viktiga begrepp när du skapar och utvärderar policyer:

* [Adobe Experience Platform datastyrning](../home.md): Den ram som [!DNL Platform] regelefterlevnad för dataanvändning.
   * [Dataanvändningsetiketter](../labels/overview.md): Dataanvändningsetiketter används i XDM-datafält, vilket anger begränsningar för hur data kan nås.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Innan du startar den här självstudiekursen bör du gå igenom [utvecklarhandbok](../api/getting-started.md) för viktig information som du behöver känna till för att kunna ringa [!DNL Policy Service] API, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Definiera en marknadsföringsåtgärd {#define-action}

I datastyrningsramverket är en marknadsföringsåtgärd en åtgärd som [!DNL Experience Platform] dataförbrukare tar, för vilka det finns ett behov av att kontrollera om dataanvändningsprinciper har överträtts.

Det första steget i att skapa en dataanvändningspolicy är att avgöra vilken marknadsföringsåtgärd som principen ska utvärdera. Detta kan du göra med något av följande alternativ:

* [Slå upp en befintlig marknadsföringsåtgärd](#look-up)
* [Skapa en ny marknadsföringsåtgärd](#create-new)

### Slå upp en befintlig marknadsföringsåtgärd {#look-up}

Du kan slå upp befintliga marknadsföringsåtgärder som ska utvärderas av din policy genom att göra en GET-förfrågan till en av `/marketingActions` slutpunkter.

**API-format**

Beroende på om du letar efter en marknadsföringsåtgärd från [!DNL Experience Platform] eller en anpassad marknadsföringsåtgärd som har skapats av organisationen, använder `marketingActions/core` eller `marketingActions/custom` slutpunkter.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Begäran**

Följande begäran använder `marketingActions/custom` slutpunkt, som hämtar en lista över alla marknadsföringsåtgärder som definieras av din IMS-organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar det totala antalet marknadsföringsåtgärder som hittats (`count`) och visar detaljerna om marknadsföringsåtgärderna i sig inom `children` array.

```json
{
    "_page": {
        "start": "sampleMarketingAction",
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714012088,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550793833224,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `_links.self.href` | Varje objekt i `children` arrayen innehåller ett URI-ID för den listade marknadsföringsåtgärden. |

När du hittar den marknadsföringsåtgärd du vill använda ska du registrera värdet på dess `href` -egenskap. Det här värdet används under nästa steg i [skapa en profil](#create-policy).

### Skapa en ny marknadsföringsåtgärd {#create-new}

Du kan skapa en ny marknadsföringsåtgärd genom att göra en PUT-förfrågan till `/marketingActions/custom/` slutpunkt och ange ett namn för marknadsföringsåtgärden i slutet av sökvägen.

**API-format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den nya marknadsföringsåtgärd som du vill skapa. Det här namnet fungerar som marknadsföringsåtgärdens primära identifierare och måste därför vara unikt. Det bästa sättet är att ge marknadsföringsåtgärden ett namn som är beskrivande men koncist. |

**Begäran**

Följande begäran skapar en ny anpassad marknadsföringsåtgärd som kallas&quot;exportToThirdParty&quot;. Observera att `name` i nyttolasten för begäran är samma som namnet i sökvägen för begäran.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "exportToThirdParty",
      "description": "Export data to a third party"
    }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på den marknadsföringsåtgärd som du vill skapa. Det här namnet måste matcha det namn som anges i sökvägen till begäran, annars inträffar ett 400-fel (Ogiltig begäran). |
| `description` | En läsbar beskrivning av marknadsföringsåtgärden. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyligen skapade marknadsföringsåtgärden.

```json
{
    "name": "exportToThirdParty",
    "description": "Export data to a third party",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "{CREATED_CLIENT}",
    "createdUser": "{CREATED_USER",
    "updated": 1550713856390,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
        }
    }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `_links.self.href` | URI-ID för marknadsföringsåtgärden. |

Registrera URI-ID:t för den nyligen skapade marknadsföringsåtgärden, så som det kommer att användas i nästa steg i skapandet av en profil.

## Skapa en profil {#create-policy}

Om du skapar en ny princip måste du tillhandahålla URI-ID:t för en marknadsföringsåtgärd med ett uttryck för användningsetiketterna som förbjuder den marknadsföringsåtgärden.

Det här uttrycket kallas ett principuttryck och är ett objekt som innehåller antingen (A) en etikett eller (B) en operator och operander, men inte båda. I sin tur är varje operand också ett principuttrycksobjekt. En policy för export av data till en tredje part kan till exempel vara förbjuden om `C1 OR (C3 AND C7)` etiketter finns. Detta uttryck skulle anges som:

```json
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
}
```

>[!NOTE]
>
>Endast operatorerna OR och AND stöds.

När du har konfigurerat ditt principuttryck kan du skapa en ny princip genom att göra en begäran om POST till `/policies/custom` slutpunkt.

**API-format**

```http
POST /policies/custom
```

**Begäran**

I följande begäran skapas en princip som heter&quot;Exportera data till tredje part&quot; genom att en marknadsföringsåtgärd och ett policyuttryck tillhandahålls i nyttolasten för begäran.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Egenskap | Beskrivning |
| --- | --- |
| `marketingActionRefs` | En array som innehåller `href` värdet av en marknadsföringsåtgärd som erhållits i [föregående steg](#define-action). I exemplet ovan anges endast en marknadsföringsåtgärd, men flera åtgärder kan också anges. |
| `deny` | Principuttrycksobjektet. Definierar de användningsetiketter och villkor som skulle få principen att avvisa den marknadsföringsåtgärd som refereras i `marketingActionRefs`. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nya principen.

```json
{
    "name": "Export Data to Third Party",
    "status": "DRAFT",
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
    "updated": 1565651746693,
    "updatedClient": "{UPDATED_CLIENT}",
    "updatedUser": "{UPDATED_USER}",
    "_links": {
        "self": {
            "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
    },
    "id": "5d51f322e553c814e67af1a3"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Ett skrivskyddat systemgenererat värde som unikt identifierar principen. |

Registrera URI-ID:t för den nyligen skapade principen så som den används i nästa steg för att aktivera principen.

## Aktivera profilen

>[!NOTE]
>
>Det här steget är valfritt om du vill lämna din policy i `DRAFT` status, observera att en policy som standard måste ha sin status inställd på `ENABLED` för att delta i utvärderingen. Se guiden [policytillämpning](../enforcement/api-enforcement.md) om du vill ha information om hur du gör undantag för policyer i `DRAFT` status.

Som standard har profiler sina `status` egenskap inställd på `DRAFT` inte deltar i utvärderingen. Du kan aktivera din policy för utvärdering genom att göra en PATCH-förfrågan till `/policies/custom/` slutpunkt och ange den unika identifieraren för principen i slutet av sökvägen för begäran.

**API-format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | The `id` värdet för profilen som du vill aktivera. |

**Begäran**

Följande begäran utför en PATCH-åtgärd på `status` egenskap för principen, ändra dess värde från `DRAFT` till `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    {
      "op": "replace",
      "path": "/status",
      "value": "ENABLED"
    }
  ]'
```

| Egenskap | Beskrivning |
| --- | --- |
| `op` | Den typ av PATCH-åtgärd som ska utföras. Denna begäran utför en ersättningsåtgärd. |
| `path` | Sökvägen till det fält som ska uppdateras. När du aktiverar en princip måste värdet anges till /status. |
| `value` | Det nya värdet som ska tilldelas till egenskapen som anges i `path`. Denna begäran anger principens `status` till ENABLED. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och information om den uppdaterade principen, med dess `status` nu inställt på `ENABLED`.

```json
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
    "createdUser": "{CREATED_USER}",
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
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en dataanvändningspolicy för en marknadsföringsåtgärd. Nu kan du fortsätta med självstudiekursen på [tillämpa dataanvändningsprinciper](../enforcement/api-enforcement.md) om du vill lära dig hur du söker efter policyöverträdelser och hur du hanterar dem i ditt upplevelseprogram.

Mer information om olika tillgängliga åtgärder finns i [!DNL Policy Service] API, se [Utvecklarhandbok för principtjänst](../api/getting-started.md). Mer information om hur du tillämpar regler för [!DNL Real-Time Customer Profile] data, se självstudiekursen om [se till att dataanvändningen efterlevs för målgruppssegment](../../segmentation/tutorials/governance.md).

Så här hanterar du användarprofiler i [!DNL Experience Platform] -användargränssnittet finns i [principanvändarhandbok](user-guide.md).
