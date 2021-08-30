---
title: Företagets slutpunkt
description: Lär dig hur du anropar slutpunkten /companies i Reactor API.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# Företagets slutpunkt

Ett företag representerar en kundorganisation, vanligtvis en verksamhet. I Reactor API matchar de här företagen 1:1 med IMS Organization ID. API-användare har bara insyn i de företag som de har tillgång till. Ett företag kan innehålla många [egenskaper](./properties.md). En egenskap tillhör exakt ett företag.

Med slutpunkten `/companies` i Reaktors-API kan du hämta de företag som du har tillgång till i ditt upplevelseprogram programmatiskt.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta en lista över företag {#list}

Du kan lista de företag som du har behörighet att använda genom att göra en GET-förfrågan till `/companies`-slutpunkten. I de flesta fall finns det precis en.

**API-format**

```http
GET /companies
```

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade företag filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Mer information finns i guiden [filtrera svar](../guides/filtering.md).

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista över företag som du har tillgång till.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{IMS_ORG}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## Hitta ett företag {#lookup}

Du kan söka efter ett visst företag genom att ta med dess ID i sökvägen för en GET-förfrågan.

**API-format**

```http
GET /companies/{COMPANY_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{COMPANY_ID}` | Värdet `id` för det företag du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar information om företaget.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{IMS_ORG}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
