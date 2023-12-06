---
keywords: Experience Platform;hem;populära ämnen;filter;Filter;filterdata;Filterdata
solution: Experience Platform
title: Lista katalogobjekt
description: Du kan hämta en lista över alla tillgängliga objekt av en viss typ via ett enda API-anrop. Det bästa sättet är att ta med filter som begränsar svarsstorleken.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
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
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska listas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | En frågeparameter som används för att filtrera resultaten som returneras i svaret. Flera parametrar avgränsas med et-tecken (`&`). Se guiden på [filtrera katalogdata](filter-data.md) för mer information. |

**Begäran**

Exempelbegäran nedan hämtar en lista med datauppsättningar, med en `limit` filtrera och reducera svaret till fem resultat, samt `properties` filter som begränsar de egenskaper som visas för varje datauppsättning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med [!DNL Catalog] objekt i form av nyckelvärdepar, filtrerade efter frågeparametrarna som anges i begäran. För varje nyckelvärdepar representerar nyckeln en unik identifierare för [!DNL Catalog] objektet i fråga, som sedan kan användas i ett annat anrop till [visa det specifika objektet](look-up-object.md) för mer information.

>[!NOTE]
>
>Om ett returnerat objekt inte innehåller en eller flera av de begärda egenskaperna som anges av `properties` -frågan returnerar bara de begärda egenskaperna som det innehåller, vilket visas i ***`Sample Dataset 3`*** och ***`Sample Dataset 4`*** nedan.

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
