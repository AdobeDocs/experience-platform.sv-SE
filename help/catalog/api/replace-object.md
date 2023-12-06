---
keywords: Experience Platform;hem;populära ämnen;katalog;api;ersätt ett objekt
solution: Experience Platform
title: Ersätta ett katalogobjekt
description: Du kan skriva över innehållet i ett Catalog-objekt med hjälp av en PUT-begäran, där hela resursen ersätts med nyttolasten för begäran.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Ersätta ett katalogobjekt

Du kan skriva över innehållet i en [!DNL Catalog] objekt som använder en PUT-begäran, där hela resursen ersätts med den begärda nyttolasten.

>[!NOTE]
>
>Om du bara behöver uppdatera ett fåtal specifika fält i en [!DNL Catalog] kan det vara mer effektivt att använda en PATCH-begäran.

**API-format**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska ersättas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran skriver över en datauppsättning med värdena som anges i nyttolasten.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för det överskrivna objektet. Detta ID ska matcha det som skickades i PUT-begäran. När en GET-förfrågan utförs för det här objektet visas nu att dess information har ersatts med den som fanns i nyttolasten för den tidigare PUT-begäran.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
