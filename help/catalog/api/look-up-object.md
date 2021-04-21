---
keywords: Experience Platform;hem;populära ämnen;katalog;objektsökning;api
solution: Experience Platform
title: Söka efter ett katalogobjekt
topic-legacy: developer guide
description: Om du känner till den unika identifieraren för ett specifikt katalogobjekt kan du utföra en GET-förfrågan för att visa objektets information.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
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
| `{OBJECT_TYPE}` | Typen för [!DNL Catalog]-objektet som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill hämta. |

**Begäran**

Följande begäran hämtar en datauppsättning med dess ID och returnerar egenskaperna `name`, `description`, `state`, `tags` och `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar den angivna datauppsättningen med endast den begärda `properties` i brödtexten.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>Egenskaper vars värden har prefixet `@` representerar relaterade objekt. I avsnittet med bilagor i [vyn över relaterade objekt](appendix.md#view-interrelated-objects) finns anvisningar om hur du visar information om dessa objekt.
