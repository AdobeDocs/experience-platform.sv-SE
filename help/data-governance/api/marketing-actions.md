---
keywords: Experience Platform;hemmabruk;populära ämnen;Politiska åtgärder;marknadsföringsåtgärder api;API-baserad tillämpning;datastyrning
solution: Experience Platform
title: API-slutpunkt för marknadsföringsåtgärder
topic: developer guide
description: En marknadsföringsåtgärd, inom ramen för Adobe Experience Platform Data Governance, är en åtgärd som en datakonsument i Experience Platform vidtar och där det finns ett behov av att kontrollera om dataanvändningspolicyer har överträtts.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Slutpunkt för marknadsföringsåtgärder

En marknadsföringsåtgärd, i samband med Adobe Experience Platform [!DNL Data Governance], är en åtgärd som en [!DNL Experience Platform]-datakonsument utför, och där det finns ett behov av att kontrollera om dataanvändningsprinciper har efterlevts.

Du kan hantera marknadsföringsåtgärder för organisationen med slutpunkten `/marketingActions` i principtjänstens API.

## Komma igång

API-slutpunkterna som används i den här guiden är en del av [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform]-API.

## Hämta en lista med marknadsföringsåtgärder {#list}

Du kan hämta en lista över viktiga eller anpassade marknadsföringsåtgärder genom att göra en GET-förfrågan till `/marketingActions/core` eller `/marketingActions/custom`.

**API-format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Begäran**

Följande begäran hämtar en lista över anpassade marknadsföringsåtgärder som hanteras av din organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information för varje hämtad marknadsföringsåtgärd, inklusive dess `name` och `href`. Värdet `href` används för att identifiera marknadsföringsåtgärden när [en dataanvändningsprincip](policies.md#create-policy) skapas.

```json
{
    "_page": {
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
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `_page.count` | Det totala antalet returnerade marknadsföringsåtgärder. |
| `children` | En array med objekt som innehåller information om hämtade marknadsföringsåtgärder. |
| `name` | Namnet på marknadsföringsåtgärden, som fungerar som sin unika identifierare när [söker efter en specifik marknadsföringsåtgärd](#lookup). |
| `_links.self.href` | En URI-referens för marknadsföringsåtgärden, som kan användas för att slutföra matrisen `marketingActionsRefs` när [en dataanvändningsprincip](policies.md#create-policy) skapas. |

## Slå upp en specifik marknadsföringsåtgärd {#lookup}

Du kan hitta detaljerna om en viss marknadsföringsåtgärd genom att ta med marknadsföringsåtgärdens `name`-egenskap i sökvägen till en GET-förfrågan.

**API-format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Egenskapen `name` för den marknadsföringsåtgärd som du vill söka efter. |

**Begäran**

Följande begäran hämtar en anpassad marknadsföringsåtgärd med namnet `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektet innehåller information om marknadsföringsåtgärden, inklusive sökvägen (`_links.self.href`) som behövs för att referera till marknadsföringsåtgärden när [en dataanvändningspolicy](policies.md#create-policy) (`marketingActionsRefs`) definieras.

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## Skapa eller uppdatera en anpassad marknadsföringsåtgärd {#create-update}

Du kan skapa en ny anpassad marknadsföringsåtgärd, eller uppdatera en befintlig, genom att ta med marknadsföringsåtgärdens befintliga eller avsedda namn i sökvägen till en PUT-förfrågan.

**API-format**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som ska skapas eller uppdateras. Om det redan finns en marknadsföringsåtgärd med det angivna namnet i systemet uppdateras den marknadsföringsåtgärden. Om det inte finns någon sådan, skapas en ny marknadsföringsåtgärd för det angivna namnet. |

**Begäran**

Följande begäran skapar en ny marknadsföringsåtgärd med namnet `crossSiteTargeting`, förutsatt att det inte finns någon marknadsföringsåtgärd med samma namn i systemet än. Om det finns en `crossSiteTargeting`-marknadsföringsåtgärd uppdaterar det här anropet i stället marknadsföringsåtgärden baserat på de egenskaper som anges i nyttolasten.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på den marknadsföringsåtgärd som ska skapas eller uppdateras. <br><br>**VIKTIGT**: Den här egenskapen måste matcha  `{MARKETING_ACTION_NAME}` i sökvägen, annars inträffar ett HTTP 400-fel (Ogiltig begäran). När en marknadsföringsåtgärd har skapats kan egenskapen `name` alltså inte ändras. |
| `description` | En valfri beskrivning som ger ytterligare sammanhang för marknadsföringsåtgärden. |

**Svar**

Ett lyckat svar returnerar detaljerna om marknadsföringsåtgärden. Om en befintlig marknadsföringsåtgärd uppdaterades returnerar svaret HTTP-status 200 (OK). Om en ny marknadsföringsåtgärd skapades returnerar svaret HTTP-status 201 (Skapad).

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## Ta bort en anpassad marknadsföringsåtgärd {#delete}

Du kan ta bort en anpassad marknadsföringsåtgärd genom att ta med dess namn i sökvägen för en DELETE-begäran.

>[!NOTE]
>
>Marknadsföringsåtgärder som refereras av befintliga principer kan inte tas bort. Om du försöker ta bort en av dessa marknadsföringsåtgärder genereras ett HTTP 400-fel (felaktig begäran) tillsammans med ett meddelande som innehåller ID:n för alla profiler som refererar till marknadsföringsåtgärden.

**API-format**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| Parameter | Beskrivning |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Namnet på den marknadsföringsåtgärd som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) med en tom svarstext.

Du kan bekräfta borttagningen genom att försöka [söka efter marknadsföringsåtgärden](#look-up). Du bör få ett HTTP 404-fel (Hittades inte) om marknadsföringsåtgärden har tagits bort från systemet.
