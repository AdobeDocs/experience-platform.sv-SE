---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbok för frågetjänstutvecklare
topic: runs for scheduled queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Körs för schemalagda frågor

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t för frågetjänsten. Följande avsnitt går igenom de olika API-anrop du kan göra med hjälp av API:t för frågetjänsten. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Hämta en lista över alla körningar för en angiven schemalagd fråga

Du kan hämta en lista över alla körningar för en viss schemalagd fråga, oavsett om de körs eller redan har slutförts. Detta görs genom att en GET-begäran görs till `/schedules/{SCHEDULE_ID}/runs` slutpunkten, där `{SCHEDULE_ID}` är `id` värdet för den schemalagda frågan vars körningar du vill hämta.

**API-format**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan som du vill hämta. |
| `{QUERY_PARAMETERS}` | (*Valfritt*) Parametrar har lagts till i sökvägen för begäran som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan. |

**Frågeparametrar**

Här följer en lista över tillgängliga frågeparametrar för att lista körningar för en angiven schemalagd fråga. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla körningar som är tillgängliga för den angivna schemalagda frågan.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. Resultatet `orderby=created` sorteras t.ex. i stigande ordning. Om du lägger till en `-` tidigare skapad (`orderby=-created`) sorteras objekt i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Förskjuter svarslistan med nollbaserad numrering. En lista `start=2` returneras till exempel från den tredje listade frågan. (*Standardvärde: 0*) |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** vara HTML-escape. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `created`, `state`och `externalTrigger`. Listan med operatorer som stöds är `>` (större än), `<` (mindre än) och `==` (lika med) och `!=` (inte lika med). Till exempel `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` returneras alla körningar som har skapats manuellt, slutförts och skapats efter den 20 april 2019. |

**Begäran**

Följande begäran hämtar de fyra sista körningarna för den angivna schemalagda frågan.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över körningar för den angivna schemalagda frågan som JSON. Följande svar returnerar de fyra sista körningarna för den angivna schemalagda frågan.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>Du kan använda värdet för `_links.cancel` att [stoppa en körning för en angiven schemalagd fråga](#immediately-stop-a-run-for-a-specific-scheduled-query).

### Starta omedelbart ut en körning för en specifik schemalagd fråga

Du kan omedelbart utlösa en körning för en angiven schemalagd fråga genom att göra en POST-begäran till `/schedules/{SCHEDULE_ID}/runs` slutpunkten, där `{SCHEDULE_ID}` är `id` värdet för den schemalagda frågan vars körning du vill utlösa.

**API-format**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### Hämta information om en körning för en specifik schemalagd fråga

Du kan hämta information om en körning för en specifik schemalagd fråga genom att göra en GET-begäran till `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` slutpunkten och ange både ID:t för den schemalagda frågan och körningen i sökvägen för begäran.

**API-format**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan vars körning du vill hämta information om. |
| `{RUN_ID}` | Värdet `id` för den körning som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna körningen.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### Stoppa omedelbart en körning för en specifik schemalagd fråga

Du kan omedelbart stoppa en körning för en specifik schemalagd fråga genom att göra en PATCH-begäran till `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` slutpunkten och ange både ID:t för den schemalagda frågan och körningen i sökvägen för begäran.

**API-format**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan vars körning du vill hämta information om. |
| `{RUN_ID}` | Värdet `id` för den körning som du vill hämta. |

**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
