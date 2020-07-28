---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en dataanvändningsprincip
topic: policies
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---


# Skapa en dataanvändningsprincip i API:t

Varumärkning och verkställighet av dataanvändning (DULE) är huvudmekanismen för Adobe Experience Platform [!DNL Data Governance]. Med API:t för [DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) kan du skapa och hantera DULE-principer för att avgöra vilka marknadsföringsåtgärder som kan vidtas mot data som innehåller vissa DULE-etiketter.

Det här dokumentet innehåller en stegvis självstudiekurs för att skapa en DULE-princip med API:t. [!DNL Policy Service] En mer utförlig guide till de olika åtgärder som är tillgängliga i API:t finns i Utvecklarhandbok för [principtjänst](../api/getting-started.md).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande viktiga koncept som används för att skapa och utvärdera DULE-policyer:

* [!DNL Data Governance](../home.md): Ramverket som [!DNL Platform] genomdriver efterlevnad av dataanvändning.
* [Dataanvändningsetiketter](../labels/overview.md): Dataanvändningsetiketter används i XDM-datafält, vilket anger begränsningar för hur data kan nås.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Innan du startar den här självstudiekursen bör du läsa igenom [utvecklarhandboken](../api/getting-started.md) för att få viktig information som du behöver känna till för att kunna anropa DULE [!DNL Policy Service] API, inklusive obligatoriska rubriker och hur du läser exempel-API-anrop.

## Definiera en marknadsföringsåtgärd {#define-action}

Inom [!DNL Data Governance] ramen är en marknadsföringsåtgärd en åtgärd som en [!DNL Experience Platform] datakonsument vidtar, och för vilken det finns ett behov av att kontrollera om dataanvändningspolicyer har överträtts.

Det första steget i att skapa en DULE-policy är att avgöra vilka marknadsföringsåtgärder som policyn kommer att utvärdera. Detta kan du göra med något av följande alternativ:

* [Slå upp en befintlig marknadsföringsåtgärd](#look-up)
* [Skapa en ny marknadsföringsåtgärd](#create-new)

### Slå upp en befintlig marknadsföringsåtgärd {#look-up}

Du kan slå upp befintliga marknadsföringsåtgärder som ska utvärderas av din DULE-policy genom att göra en GET-förfrågan till någon av `/marketingActions` slutpunkterna.

**API-format**

Beroende på om du letar upp en marknadsföringsåtgärd som tillhandahålls av [!DNL Experience Platform] eller en anpassad marknadsföringsåtgärd som har skapats av din organisation ska du använda `marketingActions/core` - eller `marketingActions/custom` -slutpunkterna.

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Begäran**

Följande begäran använder `marketingActions/custom` slutpunkten, som hämtar en lista över alla marknadsföringsåtgärder som definieras av din IMS-organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar det totala antalet marknadsföringsåtgärder som hittats (`count`) och visar information om själva marknadsföringsåtgärderna i `children` arrayen.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

När du hittar den marknadsföringsåtgärd du vill använda ska du registrera värdet på dess `href` egenskap. Det här värdet används under nästa steg när du [skapar en DULE-princip](#create-policy).

### Skapa en ny marknadsföringsåtgärd {#create-new}

Du kan skapa en ny marknadsföringsåtgärd genom att göra en PUT-begäran till `/marketingActions/custom/` slutpunkten och ange ett namn för marknadsföringsåtgärden i slutet av den begärda sökvägen.

**API-format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den nya marknadsföringsåtgärd som du vill skapa. Det här namnet fungerar som marknadsföringsåtgärdens primära identifierare och måste därför vara unikt. Det bästa sättet är att ge marknadsföringsåtgärden ett namn som är beskrivande men koncist. |

**Begäran**

Följande begäran skapar en ny anpassad marknadsföringsåtgärd som kallas&quot;exportToThirdParty&quot;. Observera att nyttolasten `name` i begäran är samma som namnet som anges i sökvägen till begäran.

```shell
curl -X PUT \  
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Registrera URI-ID:t för den nyligen skapade marknadsföringsåtgärden, så som det kommer att användas i nästa steg när du skapar en DULE-princip.

## Skapa en DULE-princip {#create-policy}

Om du skapar en ny princip måste du tillhandahålla URI-ID:t för en marknadsföringsåtgärd med ett uttryck för DULE-etiketterna som förbjuder den marknadsföringsåtgärden.

Det här uttrycket kallas ett **principuttryck** och är ett objekt som innehåller antingen (A) en DULE-etikett eller (B) en operator och operander, men inte båda. I sin tur är varje operand också ett principuttrycksobjekt. En policy för export av data till en tredje part kan till exempel vara förbjuden om det finns `C1 OR (C3 AND C7)` etiketter. Detta uttryck skulle anges som:

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

När du har konfigurerat ditt principuttryck kan du skapa en ny DULE-princip genom att göra en POST-förfrågan till `/policies/custom` slutpunkten.

**API-format**

```http
POST /policies/custom
```

**Begäran**

Följande begäran skapar en DULE-princip med namnet&quot;Exportera data till tredje part&quot; genom att tillhandahålla en marknadsföringsåtgärd och ett policyuttryck i nyttolasten för begäran.

```shell
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

| Egenskap | Beskrivning |
| --- | --- |
| `marketingActionRefs` | En array som innehåller värdet `href` för en marknadsföringsåtgärd, som du fick i [föregående steg](#define-action). I exemplet ovan anges endast en marknadsföringsåtgärd, men flera åtgärder kan också anges. |
| `deny` | Principuttrycksobjektet. Definierar DULE-etiketter och villkor som skulle få principen att avvisa den marknadsföringsåtgärd som refereras i `marketingActionRefs`. |

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
    "imsOrg": "{IMS_ORG}",
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
| `id` | Ett skrivskyddat systemgenererat värde som unikt identifierar DULE-principen. |

Registrera URI-ID:t för den nya DULE-principen så som den används i nästa steg för att aktivera principen.

## Aktivera DULE-principen

>[!NOTE]
>
>Detta steg är valfritt om du vill lämna din DULE-princip i `DRAFT` status, men tänk på att en policy som standard måste ha sin status inställd på `ENABLED` för att kunna delta i utvärderingen. Se självstudiekursen om hur du [verkställer DULE-regler](../enforcement/api-enforcement.md) för mer information om hur du gör undantag för policyer i `DRAFT` status.

Som standard deltar inte DULE-principer som har egenskapen `status` inställd på att `DRAFT` delta i utvärderingen. Du kan aktivera din princip för utvärdering genom att göra en PATCH-begäran till `/policies/custom/` slutpunkten och ange den unika identifieraren för principen i slutet av sökvägen.

**API-format**

```http
PATCH /policies/custom/{POLICY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{POLICY_ID}` | Värdet `id` för profilen som du vill aktivera. |

**Begäran**

Följande begäran utför en PATCH-åtgärd på egenskapen `status` för DULE-principen och ändrar dess värde från `DRAFT` till `ENABLED`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `value` | Det nya värdet som ska tilldelas den egenskap som anges i `path`. Den här begäran ställer in principens `status` egenskap till &quot;ENABLED&quot;. |

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och information om den uppdaterade principen, med dess `status` nu inställd på `ENABLED`.

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
    "imsOrg": "{IMS_ORG}",
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

Genom att följa den här självstudiekursen har du skapat en dataanvändningspolicy för en marknadsföringsåtgärd. Nu kan du fortsätta med självstudiekursen om hur du [verkställer dataanvändningspolicyer](../enforcement/api-enforcement.md) för att lära dig hur du söker efter regelöverträdelser och hanterar dem i ditt upplevelseprogram.

Mer information om de olika tillgängliga åtgärderna i [!DNL Policy Service] API:t finns i Utvecklarhandbok [för](../api/getting-started.md)principtjänst. Mer information om hur du tillämpar policyer för [!DNL Real-time Customer Profile] data finns i självstudiekursen om [hur ni framtvingar regelefterlevnad för målgruppssegment](../../segmentation/tutorials/governance.md).

Mer information om hur du hanterar användarprofiler i [!DNL Experience Platform] användargränssnittet finns i [principanvändarhandboken](user-guide.md).