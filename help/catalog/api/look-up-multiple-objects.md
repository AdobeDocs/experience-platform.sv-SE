---
keywords: Experience Platform;hem;populära ämnen;katalog;sökning efter flera objekt;api
solution: Experience Platform
title: Slå upp flera katalogobjekt
description: Om du vill visa flera specifika objekt, i stället för att göra en begäran per objekt, finns det en enkel genväg för att begära flera objekt av samma typ i Katalog. Du kan använda en enda GET-begäran för att returnera flera specifika objekt genom att ta med en kommaavgränsad lista med ID:n.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Söka efter flera katalogobjekt

Om du vill visa flera specifika objekt, i stället för att göra en begäran per objekt, erbjuder [!DNL Catalog] en enkel genväg för att begära flera objekt av samma typ. Du kan använda en enda GET-begäran för att returnera flera specifika objekt genom att ta med en kommaavgränsad lista med ID:n.

>[!NOTE]
>
>Även när du begär specifika [!DNL Catalog]-objekt är det ändå bra att `properties`-frågeparametern returnerar bara de egenskaper som du behöver.

**API-format**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | En identifierare för ett av de specifika objekt som du vill hämta. |

**Begäran**

Följande begäran innehåller en kommaavgränsad lista över datauppsättnings-ID samt en kommaavgränsad lista över egenskaper som ska returneras för varje datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med de angivna datauppsättningarna, som bara innehåller de begärda egenskaperna (`name`, `description` och `files`) för varje.

>[!NOTE]
>
>Om ett returnerat objekt inte innehåller en eller flera av de begärda egenskaperna som anges av `properties`-frågan, returnerar svaret endast de begärda egenskaper som det innehåller, vilket visas i ***`Sample Dataset 3`*** och ***`Sample Dataset 4`*** nedan.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
