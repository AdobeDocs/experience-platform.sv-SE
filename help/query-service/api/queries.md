---
keywords: Experience Platform;home;populära topics;query service;api guide;queries;query;Query service;
solution: Experience Platform
title: Frågar API-slutpunkt
topic-legacy: queries
description: Följande avsnitt går igenom anrop som du kan göra med slutpunkten /queries i API:t för frågetjänsten.
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Frågeslutpunkt

## Exempel på API-anrop

Följande avsnitt går igenom anrop som du kan göra med `/queries` slutpunkt i [!DNL Query Service] API. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Hämta en lista med frågor

Du kan hämta en lista över alla frågor för din IMS-organisation genom att göra en GET-förfrågan till `/queries` slutpunkt.

**API-format**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`: (*Valfritt*) Parametrar har lagts till i den begärda sökvägen som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan.

**Frågeparametrar**

Här följer en lista med tillgängliga frågeparametrar för att lista frågor. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla frågor som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. Till exempel: `orderby=created` sorterar resultaten efter att de har skapats i stigande ordning. Lägga till en `-` före skapande (`orderby=-created`) sorterar objekt efter att de har skapats i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Förskjuter svarslistan med nollbaserad numrering. Till exempel: `start=2` kommer att returnera en lista med början från den tredje listade frågan. (*Standardvärde: 0*) |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** Bli HTML rymd. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `created`, `updated`, `state`och `id`. Listan med operatorer som stöds är `>` (större än), `<` (mindre än), `>=` (större än eller lika med), `<=` (mindre än eller lika med), `==` (lika med), `!=` (inte lika med), och `~` (innehåller). Till exempel: `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` returnerar alla frågor med det angivna ID:t. |
| `excludeSoftDeleted` | Anger om en fråga som har tagits bort ska tas med. Till exempel: `excludeSoftDeleted=false` kommer **include** mjuka borttagna frågor. (*Boolean, standardvärde: true*) |
| `excludeHidden` | Anger om icke-användardrivna frågor ska visas. Värdet false kommer att anges **include** icke-användardrivna frågor, som CURSOR-definitioner, FETCH eller metadatafrågor. (*Boolean, standardvärde: true*) |

**Begäran**

Följande begäran hämtar den senaste frågan som skapats för din IMS-organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar HTTP-status 200 med en lista över frågor för den angivna IMS-organisationen som JSON. Följande svar returnerar den senaste frågan som skapats för din IMS-organisation.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### Skapa en fråga

Du kan skapa en ny fråga genom att göra en POST-förfrågan till `/queries` slutpunkt.

**API-format**

```http
POST /queries
```

**Begäran**

I följande begäran skapas en ny fråga som konfigurerats med värdena som anges i nyttolasten:

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `dbName` | Namnet på den databas som du skapar en SQL-fråga för. |
| `sql` | Den SQL-fråga som du vill skapa. |
| `name` | Namnet på SQL-frågan. |
| `description` | Beskrivningen av SQL-frågan. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om din nya fråga. När frågan har aktiverats och körts är `state` ändras från `SUBMITTED` till `SUCCESS`.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.cancel` till [avbryt din skapade fråga](#cancel-a-query).

### Hämta en fråga via ID

Du kan hämta detaljerad information om en viss fråga genom att göra en GET-förfrågan till `/queries` slutpunkt och som tillhandahåller frågans `id` värdet i begärandesökvägen.

**API-format**

```http
GET /queries/{QUERY_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_ID}` | The `id` värdet för frågan som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna frågan.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.cancel` till [avbryt din skapade fråga](#cancel-a-query).

### Avbryt en fråga

Du kan begära att få ta bort en viss fråga genom att göra en PATCH-förfrågan till `/queries` slutpunkt och som tillhandahåller frågans `id` värdet i begärandesökvägen.

**API-format**

```http
PATCH /queries/{QUERY_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_ID}` | The `id` värdet på frågan som du vill avbryta. |


**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `op` | Om du vill avbryta frågan måste du ange parametern op med värdet `cancel `. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande:

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```
