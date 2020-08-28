---
keywords: Experience Platform;home;popular topics;catalog;multiple object lookup;api
solution: Experience Platform
title: Söka efter flera objekt
topic: developer guide
description: Om du vill visa flera specifika objekt, i stället för att göra en begäran per objekt, finns det en enkel genväg för att begära flera objekt av samma typ i Katalog. Du kan använda en enda GET-begäran för att returnera flera specifika objekt genom att ta med en kommaavgränsad lista med ID:n.
translation-type: tm+mt
source-git-commit: b791e9e060d7686e8fc264c445bbfd1e01ff5987
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Söka efter flera objekt

Om du vill visa flera specifika objekt, i stället för att göra en begäran per objekt, [!DNL Catalog] är det en enkel genväg för att begära flera objekt av samma typ. Du kan använda en enda GET-begäran för att returnera flera specifika objekt genom att ta med en kommaavgränsad lista med ID:n.

>[!NOTE]
>
>Även när du begär specifika [!DNL Catalog] objekt är det fortfarande bra att `properties` fråga parametern så att den bara returnerar de egenskaper du behöver.

**API-format**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | En identifierare för ett av de specifika objekt som du vill hämta. |

**Begäran**

Följande begäran innehåller en kommaavgränsad lista över datauppsättnings-ID samt en kommaavgränsad lista över egenskaper som ska returneras för varje datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med de angivna datauppsättningarna, som bara innehåller de begärda egenskaperna (`name`, `description`och `files`) för varje.

>[!NOTE]
>
>Om ett returnerat objekt inte innehåller en eller flera av de begärda egenskaperna som anges av `properties` frågan, returnerar svaret endast de begärda egenskaper som det innehåller, vilket visas i ***`Sample Dataset 3`*** och ***`Sample Dataset 4`*** nedan.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
