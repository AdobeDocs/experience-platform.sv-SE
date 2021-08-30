---
title: Slutpunkt för appkonfigurationer
description: Lär dig hur du anropar slutpunkten /app_configurations i Reactor API.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---

# Slutpunkt för appkonfigurationer

>[!WARNING]
>
>Implementeringen av `/app_configurations`-slutpunkten börjar fungera när funktioner läggs till, tas bort och omarbetas.

Appkonfigurationer tillåter att autentiseringsuppgifter lagras och hämtas för senare bruk. Med slutpunkten `/app_configurations` i Reaktors API kan du programmässigt hantera appkonfigurationer i ditt upplevelseprogram.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta en lista med appkonfigurationer {#list}

**API-format**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beskrivning |
| --- | --- |
| `COMPANY_ID` | `id` för [företaget](./companies.md) som äger appkonfigurationerna. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade appkonfigurationer filtreras baserat på följande attribut:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Mer information finns i guiden [filtrera svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar en lista med appkonfigurationer.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Söka efter en appkonfiguration {#lookup}

Du kan söka efter en appkonfiguration genom att ange dess ID i sökvägen till en GET-begäran.

**API-format**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` för den programkonfiguration som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar information om appkonfigurationen.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Skapa en appkonfiguration {#create}

Du kan skapa en ny programkonfiguration genom att göra en POST-förfrågan.

**API-format**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parameter | Beskrivning |
| --- | --- |
| `COMPANY_ID` | `id` för [företaget](./companies.md) som du definierar appkonfigurationen under. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `platform` | Plattformen som programmet körs på (webb eller mobil). Detta avgör vilka meddelandetjänster som är tillgängliga. |
| `messaging_service` | Meddelandetjänsten som är associerad med appen, till exempel [Apple Push Notification service (APNs)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) och [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Detta avgör vilka nyckeltyper som kan användas. |
| `key_type` | Representerar det protokoll som en push-tjänstleverantör stöder och fastställer formatet för `push_credential`-objektet. När protokoll utvecklas för meddelandetjänster skapas nya `key_type`-värden som stöder de uppdaterade protokollen. |
| `push_credential` | Det faktiska autentiseringsvärdet, som är krypterat i vila. Det här fältet dekrypteras vanligtvis inte eller inkluderas i API-svar. Endast vissa Adobe-tjänster kan få ett svar som innehåller en dekrypterad push-autentiseringsuppgift. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den nya appkonfigurationen.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Uppdatera en appkonfiguration

Du kan uppdatera en programkonfiguration genom att inkludera dess ID i sökvägen för en PUT-begäran.

**API-format**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` för den programkonfiguration som du vill uppdatera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran uppdaterar `app_id` för en befintlig programkonfiguration.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | Ett objekt vars egenskaper representerar attributen som ska uppdateras för appkonfigurationen. Varje nyckel representerar det specifika programkonfigurationsattribut som ska uppdateras, tillsammans med motsvarande värde som det ska uppdateras till.<br><br>Följande attribut kan uppdateras för appkonfigurationer:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | `id` för den programkonfiguration som du vill uppdatera. Detta ska matcha `{APP_CONFIGURATION_ID}`-värdet som anges i sökvägen till begäran. |
| `type` | Den typ av resurs som uppdateras. För den här slutpunkten måste värdet vara `app_configurations`. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den uppdaterade programkonfigurationen.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Ta bort en appkonfiguration

Du kan ta bort en programkonfiguration genom att ta med dess ID i sökvägen för en DELETE-begäran.

**API-format**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `APP_CONFIGURATION_ID` | `id` för den programkonfiguration som du vill ta bort. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext, vilket anger att appkonfigurationen har tagits bort.
