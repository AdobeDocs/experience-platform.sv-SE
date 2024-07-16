---
keywords: Experience Platform;hem;populära ämnen;katalog;objektsökning;api
solution: Experience Platform
title: Söka efter ett katalogobjekt
description: Om du känner till den unika identifieraren för ett specifikt katalogobjekt kan du utföra en GET-förfrågan för att visa objektets information.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Söka efter ett katalogobjekt

Om du känner till den unika identifieraren för ett specifikt [!DNL Catalog]-objekt kan du utföra en GET-förfrågan för att visa objektets information.

>[!NOTE]
>
>När du visar specifika objekt är det fortfarande bra att [filtrera efter egenskaper](filter-data.md) och bara returnera de egenskaper som du är intresserad av.

**API-format**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill hämta. |

**Begäran**

Följande begäran hämtar en datauppsättning med dess ID och returnerar egenskaperna `name`, `description`, `tags` och `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar den angivna datauppsättningen med endast den begärda `properties` i brödtexten.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Egenskaper vars värden har prefixet `@` representerar relaterade objekt. Avsnittet i bilagan [Visa relaterade objekt](appendix.md#view-interrelated-objects) innehåller anvisningar om hur du visar information om dessa objekt.
