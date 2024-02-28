---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Frågetjänst;schemalagda frågor;schemalagd fråga;
solution: Experience Platform
title: Slutpunkt för schema
description: I följande avsnitt går du igenom de olika API-anrop du kan göra för schemalagda frågor med API:t för frågetjänsten.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 0%

---

# Slutpunkt för scheman

## Exempel på API-anrop

Nu när du förstår vilka rubriker du ska använda kan du börja ringa till [!DNL Query Service] API. Följande avsnitt går igenom de olika API-anropen som du kan göra med [!DNL Query Service] API. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

### Hämta en lista med schemalagda frågor

Du kan hämta en lista över alla schemalagda frågor för din organisation genom att göra en GET-förfrågan till `/schedules` slutpunkt.

**API-format**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*Valfritt*) Parametrar har lagts till i den begärda sökvägen som konfigurerar resultaten som returneras i svaret. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`). De tillgängliga parametrarna visas nedan. |

**Frågeparametrar**

Här följer en lista med tillgängliga frågeparametrar för att lista schemalagda frågor. Alla dessa parametrar är valfria. Om du anropar den här slutpunkten utan parametrar hämtas alla schemalagda frågor som är tillgängliga för din organisation.

| Parameter | Beskrivning |
| --------- | ----------- |
| `orderby` | Anger fältet som resultaten ska sorteras efter. De fält som stöds är `created` och `updated`. Till exempel: `orderby=created` sorterar resultaten efter att de har skapats i stigande ordning. Lägga till en `-` före skapande (`orderby=-created`) sorterar objekt efter att de har skapats i fallande ordning. |
| `limit` | Anger sidstorleksgränsen för att styra antalet resultat som ska inkluderas på en sida. (*Standardvärde: 20*) |
| `start` | Ange en tidsstämpel för ISO-format för att beställa resultaten. Om inget startdatum anges returnerar API-anropet den äldsta schemalagda frågan först och fortsätter sedan att visa de senaste resultaten.<br> ISO-tidsstämplar tillåter olika nivåer av granularitet för datum och tid. De grundläggande ISO-tidsstämplarna har formatet: `2020-09-07` för att uttrycka datumet 7 september 2020. Ett mer komplext exempel skulle skrivas som `2022-11-05T08:15:30-05:00` och motsvarar 5 november 2022, 8:15:30.00, US Eastern Standard Time. En tidszon kan anges med en UTC-förskjutning och markeras med suffixet &quot;Z&quot; (`2020-01-01T01:01:01Z`). Om ingen tidszon anges är standardvärdet noll. |
| `property` | Filtrera resultat baserat på fält. Filtren **måste** Bli HTML rymd. Kommandon används för att kombinera flera uppsättningar filter. De fält som stöds är `created`, `templateId`och `userId`. Listan med operatorer som stöds är `>` (större än), `<` (mindre än), och `==` (lika med). Till exempel: `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` returnerar alla schemalagda frågor där användar-ID:t är angivet. |

**Begäran**

Följande begäran hämtar den senaste schemalagda frågan som har skapats för din organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över schemalagda frågor för den angivna organisationen. Följande svar returnerar den senaste schemalagda frågan som skapats för din organisation.

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

Du kan skapa en ny schemalagd fråga genom att göra en POST-förfrågan till `/schedules` slutpunkt. När du skapar en schemalagd fråga i API:t kan du även se den i Frågeredigeraren. Mer information om schemalagda frågor i användargränssnittet finns i [Dokumentation för Frågeredigeraren](../ui/user-guide.md#scheduled-queries).

**API-format**

```http
POST /schedules
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `schedule.schedule` | Kronschemat för frågan. Mer information om kundscheman finns i [cron, uttrycksformat](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) dokumentation. I det här exemplet betyder &quot;30 * * *&quot; att frågan kommer att köras varje timme vid 30 minuters markering.<br><br>Du kan också använda följande kortkommandouttryck:<ul><li>`@once`: Frågan körs bara en gång.</li><li>`@hourly`: Frågan körs varje timme i början av timmen. Detta motsvarar cron-uttrycket `0 * * * *`.</li><li>`@daily`: Frågan körs en gång om dagen vid midnatt. Detta motsvarar cron-uttrycket `0 0 * * *`.</li><li>`@weekly`: Frågan körs en gång i veckan, på söndag, vid midnatt. Detta motsvarar cron-uttrycket `0 0 * * 0`.</li><li>`@monthly`: Frågan körs en gång i månaden, den första dagen i månaden, vid midnatt. Detta motsvarar cron-uttrycket `0 0 1 * *`.</li><li>`@yearly`: Frågan körs en gång per år, den 1 januari, vid midnatt. Detta motsvarar cron-uttrycket `1 0 0 1 1 *`. |
| `schedule.startDate` | Startdatumet för den schemalagda frågan, skrivet som en UTC-tidsstämpel. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om din nyligen skapade schemalagda fråga. När den schemalagda frågan har aktiverats, `state` ändras från `REGISTERING` till `ENABLED`.

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
>Du kan använda värdet för `_links.delete` till [ta bort din skapade schemalagda fråga](#delete-a-specified-scheduled-query).

### Begär information om en angiven schemalagd fråga

Du kan hämta information för en viss schemalagd fråga genom att göra en GET-förfrågan till `/schedules` slutpunkt och ange dess ID i sökvägen för begäran.

**API-format**

```http
GET /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` värdet för den schemalagda fråga som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Du kan använda värdet för `_links.delete` till [ta bort din skapade schemalagda fråga](#delete-a-specified-scheduled-query).

### Uppdatera information om en angiven schemalagd fråga

Du kan uppdatera informationen för en viss schemalagd fråga genom att göra en PATCH-förfrågan till `/schedules` slutpunkten och genom att ange dess ID i sökvägen för begäran.

Begäran från PATCH stöder två olika sökvägar: `/state` och `/schedule/schedule`.

### Uppdatera status för schemalagd fråga

Du kan uppdatera tillståndet för den valda schemalagda frågan genom att ställa in `path` egenskap till `/state` och `value` egenskap som antingen `enable` eller `disable`.

**API-format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` värdet för den schemalagda fråga som du vill PATCH. |


**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Åtgärden som ska utföras i frågeschemat. Godkänt värde är `replace`. |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet för `path` till `/state`. |
| `value` | Det uppdaterade värdet för `/state`. Detta värde kan antingen anges som `enable` eller `disable` för att aktivera eller inaktivera den schemalagda frågan. |

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med följande meddelande.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### Uppdatera schemalagt frågeschema

Du kan uppdatera cron-schemat för den schemalagda frågan genom att ange `path` egenskap till `/schedule/schedule` i begärandetexten. Mer information om kundscheman finns i [cron, uttrycksformat](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) dokumentation.

**API-format**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` värdet för den schemalagda fråga som du vill PATCH. |

**Begäran**

Denna API-begäran använder JSON Patch-syntaxen för sin nyttolast. Mer information om hur JSON Patch fungerar finns i dokumentet om grundläggande API:er.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Åtgärden som ska utföras i frågeschemat. Godkänt värde är `replace`. |
| `path` | Sökvägen för det värde som du vill laga. I det här fallet måste du ange värdet för `path` till `/schedule/schedule`. |
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

Du kan ta bort en angiven schemalagd fråga genom att göra en DELETE-förfrågan till `/schedules` slutpunkt och ange ID:t för den schemalagda fråga som du vill ta bort i sökvägen för begäran.

>[!NOTE]
>
>Schemat **måste** inaktiveras innan de tas bort.

**API-format**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{SCHEDULE_ID}` | The `id` värdet för den schemalagda fråga som du vill DELETE. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
