---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Uppdatera ett objekt
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# Uppdatera ett objekt

Du kan uppdatera en del av ett [!DNL Catalog] objekt genom att ta med dess ID i sökvägen för en PATCH-begäran. Det här dokumentet innehåller två metoder för att utföra PATCH-åtgärder på katalogobjekt:

* Använda fält
* Använda JSON Patch-notation

>[!NOTE]
>
>PATCH-åtgärder för ett objekt kan inte ändra dess utökningsbara fält, som representerar relaterade objekt.  Ändringar av sammanhörande objekt måste göras direkt.

## Uppdatera med fält

I följande exempelanrop visas hur du uppdaterar ett objekt med hjälp av fält och värden.

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog] objekt som ska uppdateras. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar fälten `name` och `description` för en datauppsättning till värdena som anges i nyttolasten. Objektfält som inte ska uppdateras kan uteslutas från nyttolasten.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickas i PATCH-begäran. När du utför en GET-begäran för den här datauppsättningen visas nu att bara `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Uppdatera med JSON Patch-notation

Följande exempelanrop visar hur du uppdaterar ett objekt med JSON Patch, enligt beskrivningen i [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog] objekt som ska uppdateras. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar fälten `name` och `description` för en datauppsättning till de värden som anges i varje JSON Patch-objekt. När du använder JSON Patch måste du även ange Content-Type-huvudet till `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för det uppdaterade objektet. Detta ID ska matcha det som skickas i PATCH-begäran. När du utför en GET-begäran för det här objektet visas nu att bara `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
