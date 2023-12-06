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

Om du känner till den unika identifieraren för en specifik [!DNL Catalog] kan du utföra en GET-begäran för att visa information om det objektet.

>[!NOTE]
>
>När du visar specifika objekt är det fortfarande bäst att [filtrera efter egenskaper](filter-data.md) och returnerar bara de egenskaper du är intresserad av.

**API-format**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identifieraren för det specifika objekt som du vill hämta. |

**Begäran**

Följande begäran hämtar en datauppsättning med dess ID och returnerar dess `name`, `description`, `tags`och `files` egenskaper.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar den angivna datauppsättningen med endast den begärda `properties` i kroppen.

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
>Egenskaper vars värden har prefixet `@` representerar relaterade objekt. Se avsnittet om bilagan [visa relaterade objekt](appendix.md#view-interrelated-objects) för steg om hur du visar information om dessa objekt.
