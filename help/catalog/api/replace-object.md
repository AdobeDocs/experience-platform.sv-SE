---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ersätta ett objekt
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Ersätta ett objekt

Du kan skriva över innehållet i ett [!DNL Catalog] objekt med en PUT-begäran, där hela resursen ersätts med den begärda nyttolasten.

>[!NOTE]
>
>Om du bara behöver uppdatera ett fåtal specifika fält i ett [!DNL Catalog] objekt kan det vara mer effektivt att använda en PATCH-begäran.

**API-format**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog] objekt som ska ersättas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill uppdatera. |

**Begäran**

Följande begäran skriver över en datauppsättning med värdena som anges i nyttolasten.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Svar**

Ett lyckat svar returnerar en array som innehåller ID:t för det överskrivna objektet. Detta ID ska matcha det som skickas i PUT-begäran. När du utför en GET-begäran för det här objektet visas nu att dess information har ersatts med den som fanns i nyttolasten för den föregående PUT-begäran.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
