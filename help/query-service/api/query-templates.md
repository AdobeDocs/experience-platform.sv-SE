---
keywords: Experience Platform;home;populära topics;query service;query templates;api guide;templates;Query service;
solution: Experience Platform
title: Frågemallar för API-slutpunkt
description: Den här guiden beskriver de olika API-anrop för frågemallar som du kan göra med hjälp av API:t för frågetjänsten.
role: Developer
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# Frågemallar, slutpunkt

## Exempel på API-anrop

I följande avsnitt beskrivs de olika API-anrop du kan göra med API:t [!DNL Query Service]. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

Mer information om hur du skapar mallar med användargränssnittet i Experience Platform finns i [dokumentationen för användargränssnittsmallar](../ui/query-templates.md).

### Hämta en lista med frågemallar

Du kan hämta en lista med alla frågemallar för din organisation genom att göra en GET-förfrågan till slutpunkten `/query-templates`.

**API-format**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Valfritt*) Parametrar har lagts till i sökvägen för begäran som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan. |

**Frågeparametrar**

Här följer en lista med tillgängliga frågeparametrar för att lista frågemallar. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla frågemallar som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. `orderby=created` sorterar till exempel resultat efter skapade i stigande ordning. Om du lägger till en `-` före skapad (`orderby=-created`) sorteras objekt efter att de har skapats i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Ange en tidsstämpel för ISO-format för att beställa resultaten. Om inget startdatum anges returnerar API-anropet de äldsta mallarna först och fortsätter sedan att visa de senaste resultaten.<br> ISO-tidsstämplar tillåter olika nivåer av granularitet för datum och tid. Grundläggande ISO-tidsstämplar har formatet `2020-09-07` för att uttrycka datumet 7 september 2020. Ett mer komplext exempel skrivs som `2022-11-05T08:15:30-05:00` och motsvarar 5 november 2022, 8:15:30 am, US Eastern Standard Time. En tidszon kan anges med en UTC-förskjutning och anges med suffixet Z (`2020-01-01T01:01:01Z`). Om ingen tidszon anges är standardvärdet noll. |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** vara HTML escape. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `name` och `userId`. Den enda operatorn som stöds är `==` (lika med). `name==my_template` returnerar till exempel alla frågemallar med namnet `my_template`. |

**Begäran**

Följande begäran hämtar den senaste frågemallen som har skapats för din organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar HTTP-status 200 med en lista över frågemallar för den angivna organisationen. Följande svar returnerar den senaste frågemallen som har skapats för din organisation.

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
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
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
>Du kan använda värdet för `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Skapa en frågemall

Du kan skapa en frågemall genom att göra en POST-förfrågan till slutpunkten `/query-templates`.

**API-format**

```http
POST /query-templates
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sql` | Den SQL-fråga som du vill skapa. Du kan antingen använda standard-SQL eller en parameterersättning. Om du vill använda en parameterersättning i SQL måste du lägga till en `$` som prefix i parameternyckeln. `$key`, till exempel, och ange parametrarna som används i SQL som JSON-nyckelvärdepar i fältet `queryParameters`. De värden som skickas här är standardparametrarna som används i mallen. Om du vill åsidosätta de här parametrarna måste du åsidosätta dem i POSTEN. |
| `name` | Namnet på frågemallen. |
| `queryParameters` | Ett nyckelvärdepar som ersätter parametriserade värden i SQL-satsen. Det krävs bara **om** du använder parameterersättningar i den SQL som du anger. Ingen värdetypskontroll utförs för dessa nyckelvärdepar. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om den nya frågemallen.

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Hämta en angiven frågemall

Du kan hämta en specifik frågemall genom att göra en GET-begäran till `/query-templates/{TEMPLATE_ID}`-slutpunkten och ange ID:t för frågemallen i begärandesökvägen.

**API-format**

```http
GET /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | Värdet `id` för den frågemall som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Uppdatera en angiven frågemall

Du kan uppdatera en viss frågemall genom att göra en PUT-begäran till `/query-templates/{TEMPLATE_ID}`-slutpunkten och ange ID:t för frågemallen i sökvägen för begäran.

**API-format**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Värdet `id` för den frågemall som du vill hämta. |

**Begäran**

>[!NOTE]
>
>Begäran från PUT kräver att både SQL- och namnfältet fylls i och **skriver över** det aktuella innehållet i frågemallen.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `sql` | Den SQL-fråga som du vill skapa. Du kan antingen använda standard-SQL eller en parameterersättning. Om du vill använda en parameterersättning i SQL måste du lägga till en `$` som prefix i parameternyckeln. `$key`, till exempel, och ange parametrarna som används i SQL som JSON-nyckelvärdepar i fältet `queryParameters`. De värden som skickas här är standardparametrarna som används i mallen. Om du vill åsidosätta de här parametrarna måste du åsidosätta dem i POSTEN. |
| `name` | Namnet på frågemallen. |
| `queryParameters` | Ett nyckelvärdepar som ersätter parametriserade värden i SQL-satsen. Det krävs bara **om** du använder parameterersättningar i den SQL som du anger. Ingen värdetypskontroll utförs för dessa nyckelvärdepar. |

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.delete` för att [ta bort frågemallen](#delete-a-specified-query-template).

### Ta bort en angiven frågemall

Du kan ta bort en viss frågemall genom att göra en DELETE-begäran till `/query-templates/{TEMPLATE_ID}` och ange ID:t för frågemallen i sökvägen för begäran.

**API-format**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{TEMPLATE_ID}` | Värdet `id` för den frågemall som du vill hämta. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
