---
keywords: Experience Platform;home;populära topics;query service;Query service;alert;
title: API-slutpunkt för aviseringsprenumerationer
description: Den här handboken innehåller exempel på HTTP-begäranden och svar för de olika API-anrop som du kan göra till slutpunkten för aviseringsprenumerationer med hjälp av API:t för frågetjänsten.
source-git-commit: cab7fcfda1bd8f6462af6e631f1fcee1f354d26b
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 0%

---

# API-slutpunkt för aviseringsprenumerationer

Med Adobe Experience Platform Query Service kan du prenumerera på aviseringar för både ad hoc-frågor och schemalagda frågor. Varningar kan tas emot via e-post, i användargränssnittet för plattformen eller båda. Meddelandeinnehållet är detsamma för varningar på plattformen och e-postvarningar. Frågevarningar kan för närvarande bara prenumereras på med [API för frågetjänst](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>Om du vill få e-postaviseringar måste du först aktivera den här inställningen i användargränssnittet. Läs dokumentationen för [instruktioner om hur du aktiverar e-postaviseringar](../../observability/alerts/ui.md#enable-email-alerts).

Tabellen nedan förklarar vilka varningsmeddelanden som stöds för olika typer av frågor:

| Frågetyp | Varningstyper som stöds |
|---|---|
| Ad hoc-frågor | `success` eller `failed` exekveringar. |
| Schemalagda frågor | `start`, `success`, eller `failed` exekveringar. |

>[!NOTE]
>
>Alla frågor som inte är SELECT-frågor har stöd för aviseringsprenumerationer och du behöver inte vara frågeskapare för att prenumerera på en avisering. Andra användare kan även registrera sig för varningar om en fråga som de inte har skapat.

Följande aviseringar gäller utan en aviseringsprenumeration:

* När ett batchfrågejobb har slutförts får användarna ett meddelande.
* När varaktigheten för ett batchfrågejobb överstiger ett tröskelvärde, utlöses en varning till den person som schemalagt frågan.

>[!NOTE]
>
>Frågor som används för testning kan uteslutas från dessa aviseringar om de är korrekt konfigurerade.

## Exempel på API-anrop

Följande avsnitt går igenom de olika API-anrop du kan göra med hjälp av API:t för frågetjänsten. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

## Hämta en lista över alla aviseringar för en organisation och en sandlåda {#get-list-of-org-alert-subs}

Hämta en lista över alla aviseringar för en organisationssandlåda genom att göra en GET-begäran till `/alert-subscriptions` slutpunkt.

**API-format**

```http
GET /alert-subscriptions
```

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP 200-status och `alerts` array med sidnumrering och versionsinformation. The `alerts` arrayen innehåller information om alla varningar för en organisation och en viss sandlåda. Det finns högst tre larm tillgängliga per svar, en varning per varningstyp finns i svarsorganet.

>[!NOTE]
>
>The `alerts._links` objekt i `alerts` arrayen har trunkerats för att vara kortfattad. Ett fullständigt exempel på `alerts._links` -objektet finns i [svar på begäran om POST](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `alerts.assetId` | Det fråge-ID som associerade aviseringen med en viss fråga. |
| `alerts.id` | Namnet på aviseringen. Det här namnet genereras av larmtjänsten och används på larmpanelen. Varningsnamnet består av den mapp som innehåller varningen, `alertType`och flödes-ID. Information om tillgängliga aviseringar finns i [Dokumentation för kontrollpanelen för plattformsaviseringar](../../observability/alerts/ui.md). |
| `alerts.status` | Varningen har fyra statusvärden: `enabled`, `enabling`, `disabled`och `disabling`. En varning lyssnar antingen aktivt efter händelser, pausas för framtida bruk samtidigt som alla relevanta prenumeranter och inställningar behålls, eller så sker en övergång mellan dessa lägen. |
| `alerts.alertType` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `alerts._links` | Tillhandahåller information om tillgängliga metoder och slutpunkter som kan användas för att hämta, uppdatera, redigera eller ta bort information om detta varnings-ID. |
| `_page` | Objektet innehåller egenskaper som beskriver ordningen, storleken, det totala antalet sidor och den aktuella sidan. |
| `_links` | Objektet innehåller URI-referenser som kan användas för att hämta nästa eller föregående sida med resurser. |

## Hämta aviseringsprenumerationsinformation för en viss fråga eller ett visst schema-ID {#retrieve-all-alert-subscriptions-by-id}

Hämta aviseringsprenumerationsinformationen för ett visst fråge-ID eller schema-ID genom att göra en GET-förfrågan till `/alert-subscriptions/{QUERY_ID}` eller `/alert-subscriptions/{SCHEDULE_ID}` slutpunkt.

**API-format**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{QUERY_ID}` | ID:t för frågan som du vill returnera prenumerationsinformationen för. |
| `{SCHEDULE_ID}` | ID:t för den schemalagda fråga som du vill returnera prenumerationsinformationen för. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett godkänt svar returnerar HTTP-statusen 200 och `alerts` matris som innehåller prenumerationsinformation för tillhandahållet fråge- eller schema-ID.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `assetId` | Varningen är kopplad till detta ID. ID:t kan vara antingen ett fråge-ID eller ett schema-ID. |
| `id` | Namnet på aviseringen. Det här namnet genereras av larmtjänsten och används på larmpanelen. Varningsnamnet består av den mapp som innehåller varningen, `alertType`och flödes-ID. Information om tillgängliga aviseringar finns i [Dokumentation för kontrollpanelen för plattformsaviseringar](../../observability/alerts/ui.md). |
| `status` | Varningen har fyra statusvärden: `enabled`, `enabling`, `disabled`och `disabling`. En varning lyssnar antingen aktivt efter händelser, pausas för framtida bruk samtidigt som alla relevanta prenumeranter och inställningar behålls, eller så sker en övergång mellan dessa lägen. |
| `alertType` | Varje varning kan ha tre olika varningstyper. De är: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `subscriptions.emailNotifications` | En matris med Adobe-registrerade e-postadresser för användare som har prenumererat på att ta emot e-postmeddelanden för aviseringen. |
| `subscriptions.inContextNotifications` | En array med Adobe-registrerade e-postadresser för användare som har prenumererat på gränssnittsmeddelanden för aviseringen. |

## Hämta aviseringsprenumerationsinformation för en viss fråga eller schema-ID och aviseringstyp {#get-alert-info-by-id-and-alert-type}

Hämta aviseringsprenumerationsinformationen för ett visst ID och en viss aviseringstyp genom att göra en GET-förfrågan till `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` slutpunkt. Detta gäller för både fråge- och schemalagda fråge-ID.

**API-format**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametrar | Beskrivning |
| -------- | ----------- |
| `ALERT_TYPE` | Varje varning kan ha tre olika varningstyper. De är: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `QUERY_ID` | Den unika identifieraren för frågan som ska uppdateras. |
| `SCHEDULE_ID` | Den unika identifieraren för den schemalagda frågan som ska uppdateras. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP-statusen 200 och alla aviseringar som prenumererar på. Detta inkluderar aviserings-ID, typ av avisering, prenumerantens Adobe-registrerade e-post-ID och deras föredragna meddelandekanal.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `assetId` | Det fråge-ID som associerade aviseringen med en viss fråga. |
| `alertType` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `subscriptions` | Ett objekt som används för att skicka registrerade e-post-ID:n för Adobe som är kopplade till aviseringarna och de kanaler som användarna kommer att ta emot aviseringarna i. |
| `subscriptions.inContextNotifications` | En array med Adobe-registrerade e-postadresser för användare som har prenumererat på gränssnittsmeddelanden för aviseringen. |
| `subscriptions.emailNotifications` | En matris med Adobe-registrerade e-postadresser för användare som har prenumererat på att ta emot e-postmeddelanden för aviseringen. |

## Hämta en lista med alla aviseringar som en användare prenumererar på {#get-alert-subscription-list}

Hämta en lista med alla aviseringar som en användare prenumererar på genom att göra en GET-förfrågan till `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` slutpunkt. Svaret innehåller varningsnamn, ID:n, status, varningstyp och meddelandekanaler.

**API-format**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| Parametrar | Beskrivning |
| -------- | ----------- |
| `{EMAIL_ID}` | En e-postadress som är registrerad för ett Adobe-konto används för att identifiera de användare som prenumererar på aviseringar. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 och `items` med information om de aviseringar som prenumererar på `emailId` tillhandahålls.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på aviseringen. Det här namnet genereras av larmtjänsten och används på larmpanelen. Varningsnamnet består av den mapp som innehåller varningen, `alertType`och flödes-ID. Information om tillgängliga aviseringar finns i [Dokumentation för kontrollpanelen för plattformsaviseringar](../../observability/alerts/ui.md). |
| `assetId` | Det fråge-ID som associerade aviseringen med en viss fråga. |
| `status` | Varningen har fyra statusvärden: `enabled`, `enabling`, `disabled`och `disabling`. En varning lyssnar antingen aktivt efter händelser, pausas för framtida bruk samtidigt som alla relevanta prenumeranter och inställningar behålls, eller så sker en övergång mellan dessa lägen. |
| `alertType` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `subscriptions` | Ett objekt som används för att skicka registrerade e-post-ID:n för Adobe som är kopplade till aviseringarna och de kanaler som användarna kommer att ta emot aviseringarna i. |
| `subscriptions.inContextNotifications` | Ett booleskt värde som avgör hur användarna får varningsmeddelanden. A `true` Värdet bekräftar att varningar ska lämnas via användargränssnittet. A `false` värdet ser till att användarna inte meddelas via den kanalen. |
| `subscriptions.emailNotifications` | Ett booleskt värde som avgör hur användarna får varningsmeddelanden. A `true` värdet bekräftar att aviseringar ska skickas via e-post. A `false` värdet ser till att användarna inte meddelas via den kanalen. |

## Skapa en avisering och prenumerera {#subscribe-users}

Om du vill skapa en avisering och prenumerera på en användare som ska ta emot den gör du en `POST` begäran till `/alert-subscriptions` slutpunkt. Denna begäran kopplar en fråga till en nyligen skapad avisering med en `assetId` och prenumererar användare på varningar för frågan med hjälp av `emailIds`.

>[!IMPORTANT]
>
>Du kan skicka upp till fem Adobe-registrerade e-post-ID:n i en enda begäran. Om du vill prenumerera för fler än fem användare på en avisering måste du göra ytterligare förfrågningar.

**API-format**

```http
POST /alert-subscriptions
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `assetId` | Varningen är kopplad till detta ID. ID:t kan vara antingen ett fråge-ID eller ett schema-ID. |
| `alertType` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `subscriptions` | Ett objekt som används för att skicka registrerade e-post-ID:n för Adobe som är kopplade till aviseringarna och de kanaler som användarna kommer att ta emot aviseringarna i. |
| `subscriptions.emailIds` | En matris med e-postadresser som identifierar de användare som ska ta emot aviseringarna. E-postadresserna **måste** vara registrerad på ett Adobe-konto. |
| `subscriptions.inContextNotifications` | Ett booleskt värde som avgör hur användarna får varningsmeddelanden. A `true` Värdet bekräftar att varningar ska lämnas via användargränssnittet. A `false` värdet ser till att användarna inte meddelas via den kanalen. |
| `subscriptions.emailNotifications` | Ett booleskt värde som avgör hur användarna får varningsmeddelanden. A `true` värdet bekräftar att aviseringar ska skickas via e-post. A `false` värdet ser till att användarna inte meddelas via den kanalen. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Accepterad) med information om din nyligen skapade avisering.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Namnet på aviseringen. Det här namnet genereras av larmtjänsten och används på larmpanelen. Varningsnamnet består av den mapp som innehåller varningen, `alertType`och flödes-ID. Information om tillgängliga aviseringar finns i [Dokumentation för kontrollpanelen för plattformsaviseringar](../../observability/alerts/ui.md). |
| `_links` | Tillhandahåller information om tillgängliga metoder och slutpunkter som kan användas för att hämta, uppdatera, redigera eller ta bort information om detta varnings-ID. |

## Aktivera eller inaktivera en varning {#enable-or-disable-alert}

Denna begäran refererar till en viss avisering med en fråga- eller schema-ID och en aviseringstyp och uppdaterar aviseringsstatusen till antingen `enable` eller `disable`. Du kan uppdatera status för en avisering genom att göra en `PATCH` begäran till `/alert-subscriptions/{queryId}/{alertType}` eller `/alert-subscriptions/{scheduleId}/{alertType}` slutpunkt.

**API-format**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametrar | Beskrivning |
| -------- | ----------- |
| `ALERT_TYPE` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul>Du måste ange den aktuella varningstypen i slutpunktens namnutrymme för att kunna ändra den. |
| `QUERY_ID` | Den unika identifieraren för frågan som ska uppdateras. |
| `SCHEDULE_ID` | Den unika identifieraren för den schemalagda frågan som ska uppdateras. |

**Begäran**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `op` | Den åtgärd som ska utföras. För närvarande är det enda godkända värdet `replace`. |
| `path` | Det här värdet relaterar till namnutrymmet i slutpunkten. För närvarande är det enda godkända värdet `/status`. |
| `value` | I en lyckad PATCH-begäran ändras `status` Varningens värde. Godkända värden är `enable` eller `disable`. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om aviseringsstatus, typ och ID samt den fråga det gäller.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Namnet på aviseringen. Det här namnet genereras av larmtjänsten och används på larmpanelen. Varningsnamnet består av den mapp som innehåller varningen, `alertType`och flödes-ID. Information om tillgängliga aviseringar finns i [Dokumentation för kontrollpanelen för plattformsaviseringar](../../observability/alerts/ui.md). |
| `assetId` | Varningen är kopplad till detta ID. ID:t kan vara antingen ett fråge-ID eller ett schema-ID. |
| `alertType` | Varje varning kan ha tre olika varningstyper. De är: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> |
| `status` | Varningen har fyra statusvärden: `enabled`, `enabling`, `disabled`och `disabling`. En varning lyssnar antingen aktivt efter händelser, pausas för framtida bruk samtidigt som alla relevanta prenumeranter och inställningar behålls, eller så sker en övergång mellan dessa lägen. |

## Ta bort aviseringen för en viss fråga och larmtyp {#delete-alert-info-by-id-and-alert-type}

Ta bort en avisering för en viss fråga eller ett visst schema-ID och en viss aviseringstyp genom att göra en DELETE-begäran till `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` eller `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` slutpunkt.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| Parametrar | Beskrivning |
| -------- | ----------- |
| `ALERT_TYPE` | Typ av varning. Det finns tre möjliga värden för en varning: <ul><li>`start`: Meddelar en användare när frågekörningen har börjat.</li><li>`success`: Meddelar användaren när frågan har slutförts.</li><li>`failure`: Meddelar användaren om frågan misslyckas.</li></ul> Begäran från DELETE gäller endast den särskilda larmtypen. |
| `QUERY_ID` | Den unika identifieraren för frågan som ska uppdateras. |
| `SCHEDULE_ID` | Den unika identifieraren för den schemalagda frågan som ska uppdateras. |

**Begäran**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP 200-status och ett bekräftelsemeddelande som innehåller resurs-ID:t och varningstypen för den borttagna varningen.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## Nästa steg

Den här guiden beskriver användningen av `/alert-subscriptions` slutpunkt i API:t för frågetjänsten. När du har läst den här guiden får du nu en bättre förståelse för hur du skapar en avisering för en fråga, prenumererar på aviseringar, vilka typer av aviseringar som är tillgängliga och hur du kan hämta, uppdatera och ta bort aviseringsprenumerationsinformation.

Se [API-guide för frågetjänst](./getting-started.md) om du vill veta mer om andra tillgängliga funktioner och åtgärder.
