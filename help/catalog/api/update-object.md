---
keywords: Experience Platform;hem;populära ämnen;katalog;api;uppdatera ett objekt
solution: Experience Platform
title: Uppdatera ett katalogobjekt
description: Du kan uppdatera en del av ett Catalog-objekt genom att ta med dess ID i sökvägen för en PATCH-begäran. Det här dokumentet innehåller information om hur du använder fält och JSON Patch-notation för att utföra PATCH-åtgärder på katalogobjekt.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 296a988a67871933723ad0474c113cb93fdbf255
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Uppdatera ett katalogobjekt

Du kan uppdatera en del av en [!DNL Catalog] genom att ta med dess ID i sökvägen för en PATCH-begäran. Det här dokumentet innehåller två metoder för att utföra PATCH-åtgärder på katalogobjekt:

* Använda fält
* Använda JSON Patch-notation

>[!NOTE]
>
>PATCH-åtgärder för ett objekt kan inte ändra dess utökningsbara fält, som representerar relaterade objekt. Ändringar av sammanhörande objekt måste göras direkt.

## Uppdatera med fält

I följande exempelanrop visas hur du uppdaterar ett objekt med hjälp av fält och värden.

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska uppdateras. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar `name` och `description` fält i en datauppsättning till de värden som anges i nyttolasten. Objektfält som inte ska uppdateras kan uteslutas från nyttolasten.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för den uppdaterade datauppsättningen. Detta ID ska matcha det som skickades i PATCH-begäran. När en GET-förfrågan utförs för den här datauppsättningen visas nu att endast `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Uppdatera med JSON Patch-notation

Följande exempelanrop visar hur du uppdaterar ett objekt med JSON Patch, enligt instruktionerna i [RFC-6902](https://tools.ietf.org/html/rfc6902).

Mer information om JSON Patch-syntaxen finns i [Grundläggande API-guide](../../landing/api-fundamentals.md#json-patch).

**API-format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska uppdateras. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar `name` och `description` fält i en datauppsättning med de värden som anges i varje JSON-lagningsobjekt. När du använder JSON Patch måste du även ange Content-Type-rubriken till `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för det uppdaterade objektet. Detta ID ska matcha det som skickades i PATCH-begäran. En GET-förfrågan för det här objektet visar nu att endast `name` och `description` har uppdaterats medan alla andra värden förblir oförändrade.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
