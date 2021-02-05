---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Frågetjänst;schemalagda frågor;schemalagd fråga;
solution: Experience Platform
title: API-slutpunkt för schemalagda frågor
topic: scheduled queries
description: I följande avsnitt går du igenom de olika API-anrop du kan göra för schemalagda frågor med API:t för frågetjänsten.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---


# Slutpunkt för schemalagda frågor

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t [!DNL Query Service]. Följande avsnitt går igenom de olika API-anrop du kan göra med API:t [!DNL Query Service]. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Hämta en lista med schemalagda frågor

Du kan hämta en lista över alla schemalagda frågor för din IMS-organisation genom att göra en GET-begäran till `/schedules`-slutpunkten.

**API-format**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Valfria*) Parametrar har lagts till i sökvägen för begäran som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan. |

**Frågeparametrar**

Här följer en lista med tillgängliga frågeparametrar för att lista schemalagda frågor. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla schemalagda frågor som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. `orderby=created` sorterar till exempel resultaten efter att de har skapats i stigande ordning. Om du lägger till en `-` före skapad (`orderby=-created`) sorteras objekten i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Förskjuter svarslistan med nollbaserad numrering. `start=2` returnerar till exempel en lista som börjar med den tredje listade frågan. (*Standardvärde: 0*) |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** vara HTML-escape. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `created`, `templateId` och `userId`. Listan med operatorer som stöds är `>` (större än), `<` (mindre än) och `==` (lika med). `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` returnerar till exempel alla schemalagda frågor där användar-ID anges. |

**Begäran**

Följande begäran hämtar den senaste schemalagda frågan som skapats för din IMS-organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över schemalagda frågor för den angivna IMS-organisationen. Följande svar returnerar den senaste schemalagda frågan som skapats för din IMS-organisation.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### Skapa en ny schemalagd fråga

Du kan skapa en ny schemalagd fråga genom att göra en POST-förfrågan till `/schedules`-slutpunkten.

**API-format**

```http
POST /schedules
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `query.dbName` | Namnet på databasen som du skapar en schemalagd fråga för. |
| `query.sql` | Den SQL-fråga som du vill skapa. |
| `query.name` | Namnet på den schemalagda frågan. |
| `schedule.schedule` | Kronschemat för frågan. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen. I det här exemplet betyder &quot;30 * * *&quot; att frågan kommer att köras varje timme vid 30 minuters markering. |
| `schedule.startDate` | Startdatumet för den schemalagda frågan, skrivet som en UTC-tidsstämpel. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om din nyligen skapade schemalagda fråga. När den schemalagda frågan har aktiverats ändras `state` från `REGISTERING` till `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` till [ta bort den schemalagda frågan](#delete-a-specified-scheduled-query) som du har skapat.

### Begär information om en angiven schemalagd fråga

Du kan hämta information för en viss schemalagd fråga genom att göra en GET-förfrågan till `/schedules`-slutpunkten och ange dess ID i sökvägen för begäran.

**API-format**

```http
GET /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den angivna schemalagda frågan.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>Du kan använda värdet `_links.delete` till [ta bort den schemalagda frågan](#delete-a-specified-scheduled-query) som du har skapat.

### Uppdatera information om en angiven schemalagd fråga

Du kan uppdatera informationen för en angiven schemalagd fråga genom att göra en PATCH-begäran till `/schedules`-slutpunkten och ange dess ID i sökvägen för begäran.

Begäran från PATCH stöder två olika sökvägar: `/state` och `/schedule/schedule`.

### Uppdatera status för schemalagd fråga

Du kan använda `/state` för att uppdatera tillståndet för den valda schemalagda frågan - ENABLED eller DISABLED. Om du vill uppdatera läget måste du ange värdet `enable` eller `disable`.

**API-format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan som du vill hämta. |


**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet `path` till `/state` eftersom du uppdaterar den schemalagda frågans tillstånd. |
| `value` | Det uppdaterade värdet för `/state`. Värdet kan antingen anges som `enable` eller `disable` för att aktivera eller inaktivera den schemalagda frågan. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Uppdatera schemalagt frågeschema

Du kan använda `/schedule/schedule` för att uppdatera schemat för kron för den schemalagda frågan. Mer information om cron-scheman finns i [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)-dokumentationen.

**API-format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan som du vill hämta. |

**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet `path` till `/schedule/schedule` eftersom du uppdaterar schemat för den schemalagda frågan. |
| `value` | Det uppdaterade värdet för `/schedule`. Värdet måste anges i form av ett kronschema. I det här exemplet körs den schemalagda frågan varje timme med 45 minuters markering. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Ta bort en angiven schemalagd fråga

Du kan ta bort en angiven schemalagd fråga genom att göra en DELETE-begäran till `/schedules`-slutpunkten och ange ID:t för den schemalagda frågan som du vill ta bort i sökvägen för begäran.

>[!NOTE]
>
>Schemat **måste** inaktiveras innan det tas bort.

**API-format**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | Värdet `id` för den schemalagda frågan som du vill hämta. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
