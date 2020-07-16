---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Marknadsföringsåtgärder
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Marknadsföringsåtgärder

En marknadsföringsåtgärd, inom ramen för Adobe Experience Platform [!DNL Data Governance], är en åtgärd som en [!DNL Experience Platform] datakonsument vidtar och där det finns ett behov av att kontrollera om dataanvändningspolicyer har överträtts.

När du arbetar med marknadsföringsåtgärder i API måste du använda `/marketingActions` slutpunkten.

## Lista alla marknadsföringsåtgärder

Om du vill visa en lista över alla marknadsföringsåtgärder kan en GET-begäran göras till `/marketingActions/core` eller `/marketingActions/custom` som returnerar alla policyer för den angivna behållaren.

**API-format**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**Begäran**

Följande begäran returnerar en lista över alla anpassade marknadsföringsåtgärder som definierats av IMS-organisationen.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Responsobjektet ger det totala antalet marknadsföringsåtgärder i behållaren (`count`) och `children` arrayen innehåller information om varje marknadsföringsåtgärd, inklusive `name` och en `href` för marknadsföringsåtgärden. Den här sökvägen (`_links.self.href`) används för att slutföra `marketingActionsRefs` arrayen när en [dataanvändningsprincip](policies.md#create-policy)skapas.

```JSON
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

## Slå upp en specifik marknadsföringsåtgärd

Du kan också utföra en sökbegäran (GET) för att visa information om en viss marknadsföringsåtgärd. Detta görs med hjälp `name` av marknadsföringsåtgärderna. Om namnet är okänt kan det hittas med den listförfrågan (GET) som visas tidigare.

**API-format**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**Begäran**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarsobjektet innehåller information om marknadsföringsåtgärden, inklusive den sökväg (`_links.self.href`) som behövs för att referera till marknadsföringsåtgärden när en dataanvändningspolicy definieras (`marketingActionsRefs`).

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

## Skapa eller uppdatera en marknadsföringsåtgärd

Med [!DNL Policy Service] API kan ni definiera egna marknadsföringsåtgärder och uppdatera befintliga. Både skapande och uppdatering görs med en PUT-åtgärd till namnet på marknadsföringsåtgärden.

**API-format**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**Begäran**

Observera i följande begäran att nyttolasten `name` i begäran är densamma som `{marketingActionName}` i API-anropet. Till skillnad från `id` en skrivskyddad och systemgenererad policy kräver en marknadsföringsåtgärd att du anger det _tänkta_ namnet på marknadsföringsåtgärden när du skapar den.

>[!NOTE]
>
>Om du inte anger värdet `{marketingActionName}` i anropet kommer det att resultera i ett 405-fel (metoden tillåts inte) eftersom du inte får utföra en PUT direkt till `/marketingActions/custom` slutpunkten. Om `name` i nyttolasten inte matchar `{marketingActionName}` i sökvägen får du dessutom ett 400-fel (felaktig begäran).

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**Svar**

Om det skapas får du en HTTP-status 201 (Skapad) och svarstexten innehåller information om den nyligen skapade marknadsföringsåtgärden. Svaret `name` i bör matcha det som skickades i begäran.

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

## Ta bort en marknadsföringsåtgärd

Det går att ta bort marknadsföringsåtgärder genom att skicka en DELETE-begäran till den `{marketingActionName}` del av marknadsföringsåtgärden som du vill ta bort.

>[!NOTE]
>
>Du kan inte ta bort marknadsföringsåtgärder som refereras av befintliga profiler. Om du försöker göra det kommer det att resultera i ett 400-fel (felaktig begäran) tillsammans med ett felmeddelande som innehåller `id` (eller flera ID:n) för en princip (eller principer) som innehåller en referens till den marknadsföringsåtgärd som du försöker ta bort.

**API-format**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**Begäran**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Om marknadsföringsåtgärden har tagits bort utan fel kommer svarstexten att vara tom med HTTP-status 200 (OK).

Du kan bekräfta borttagningen genom att försöka söka (GET) efter marknadsföringsåtgärden. Du bör få HTTP-status 404 (Hittades inte) tillsammans med felmeddelandet &quot;Hittades inte&quot; eftersom marknadsföringsåtgärden har tagits bort.
