---
keywords: Experience Platform;home;populära topics;query service;query templates;api guide;templates;Query service;
solution: Experience Platform
title: Frågemallar för API-slutpunkt
topic-legacy: query templates
description: Följande dokumentation går igenom de olika API-anrop du kan göra med hjälp av frågemallar för API:t för frågetjänsten.
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 1%

---

# Frågemallar, slutpunkt

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t [!DNL Query Service]. Följande avsnitt går igenom de olika API-anrop du kan göra med API:t [!DNL Query Service]. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Hämta en lista med frågemallar

Du kan hämta en lista med alla frågemallar för din IMS-organisation genom att göra en GET-begäran till `/query-templates`-slutpunkten.

**API-format**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Valfria*) Parametrar har lagts till i sökvägen för begäran som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan. |

**Frågeparametrar**

Här följer en lista med tillgängliga frågeparametrar för att lista frågemallar. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla frågemallar som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. `orderby=created` sorterar till exempel resultaten efter att de har skapats i stigande ordning. Om du lägger till en `-` före skapad (`orderby=-created`) sorteras objekten i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Förskjuter svarslistan med nollbaserad numrering. `start=2` returnerar till exempel en lista som börjar med den tredje listade frågan. (*Standardvärde: 0*) |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** vara HTML-escape. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `name` och `userId`. Den enda operatorn som stöds är `==` (lika med). `name==my_template` returnerar till exempel alla frågemallar med namnet `my_template`. |

**Begäran**

Följande begäran hämtar den senaste frågemallen som skapats för din IMS-organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar HTTP-status 200 med en lista över frågemallar för den angivna IMS-organisationen. Följande svar returnerar den senaste frågemallen som skapats för din IMS-organisation.

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Skapa en frågemall

Du kan skapa en frågemall genom att göra en POST-förfrågan till `/query-templates`-slutpunkten.

**API-format**

```http
POST /query-templates
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sql` | Den SQL-fråga som du vill skapa. |
| `name` | Namnet på frågemallen. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om den nya frågemallen.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Hämta en angiven frågemall

Du kan hämta en specifik frågemall genom att göra en GET-begäran till `/query-templates/{TEMPLATE_ID}`-slutpunkten och ange ID:t för frågemallen i sökvägen för begäran.

**API-format**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | `id`-värdet för den frågemall som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna frågemallen.

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Uppdatera en angiven frågemall

Du kan uppdatera en viss frågemall genom att göra en PUT-begäran till `/query-templates/{TEMPLATE_ID}`-slutpunkten och ange ID:t för frågemallen i sökvägen för begäran.

**API-format**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TEMPLATE_ID}` | `id`-värdet för den frågemall som du vill hämta. |

**Begäran**

>[!NOTE]
>
>Begäran från PUT kräver att både sql- och namnfältet fylls i, och kommer att **skriva över** det aktuella innehållet i frågemallen.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sql` | Den SQL-fråga som du vill uppdatera. |
| `name` | Namnet på den schemalagda frågan. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med den uppdaterade informationen för den angivna frågemallen.

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Ta bort en angiven frågemall

Du kan ta bort en viss frågemall genom att göra en DELETE-begäran till `/query-templates/{TEMPLATE_ID}` och ange ID:t för frågemallen i sökvägen till begäran.

**API-format**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TEMPLATE_ID}` | `id`-värdet för den frågemall som du vill hämta. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```
