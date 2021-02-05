---
keywords: Experience Platform;hem;populära ämnen;filter;Filter;filterdata;Filterdata
solution: Experience Platform
title: Lista katalogobjekt
topic: developer guide
description: Du kan hämta en lista över alla tillgängliga objekt av en viss typ via ett enda API-anrop. Det bästa sättet är att ta med filter som begränsar svarsstorleken.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Lista katalogobjekt

Du kan hämta en lista över alla tillgängliga objekt av en viss typ via ett enda API-anrop. Det bästa sättet är att ta med filter som begränsar svarsstorleken.

**API-format**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska listas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | En frågeparameter som används för att filtrera resultaten som returneras i svaret. Flera parametrar avgränsas med et-tecken (`&`). Mer information finns i guiden [filtrera katalogdata](filter-data.md). |

**Begäran**

Exempelbegäran nedan hämtar en lista med datauppsättningar, med ett `limit`-filter som reducerar svaret till fem resultat, och ett `properties`-filter som begränsar de egenskaper som visas för varje datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med [!DNL Catalog]-objekt i form av nyckelvärdepar, filtrerade med frågeparametrarna som anges i begäran. För varje nyckelvärdepar representerar nyckeln en unik identifierare för [!DNL Catalog]-objektet i fråga, som sedan kan användas i ett annat anrop till [visa det specifika objektet](look-up-object.md) för mer information.

>[!NOTE]
>
>Om ett returnerat objekt inte innehåller en eller flera av de begärda egenskaperna som anges av `properties`-frågan, returnerar svaret endast de begärda egenskaper som det innehåller, vilket visas i ***`Sample Dataset 3`*** och ***`Sample Dataset 4`*** nedan.

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
