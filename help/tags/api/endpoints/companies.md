---
title: Företagets slutpunkt
description: Lär dig hur du anropar slutpunkten /companies i Reactor API.
exl-id: ee435358-ed34-4e0c-93af-796133fb11fc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---

# Företagets slutpunkt

Ett företag representerar en kundorganisation, vanligtvis en verksamhet. I Reactor API matchar dessa företag 1:1 med organisations-ID. API-användare har bara insyn i de företag som de har tillgång till. Ett företag kan innehålla många [egenskaper](./properties.md). En egenskap tillhör exakt ett företag.

The `/companies` -slutpunkten i Reaktors API gör att du kan hämta de företag som du har tillgång till i ditt upplevelseprogram via programkod.

## Komma igång

Slutpunkten som används i den här guiden är en del av [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Läs igenom [komma igång-guide](../getting-started.md) om du vill ha viktig information om hur du autentiserar till API:t.

## Hämta en lista över företag {#list}

Du kan lista de företag som du är behörig att använda genom att göra en GET-förfrågan till `/companies` slutpunkt. I de flesta fall finns det precis en.

**API-format**

```http
GET /companies
```

>[!NOTE]
>
>Med hjälp av frågeparametrar kan listade företag filtreras baserat på följande attribut:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Se guiden [filtrera svar](../guides/filtering.md) för mer information.

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "org_id": "{ORG_ID}",
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
| `{COMPANY_ID}` | The `id` värdet på det företag du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
      "org_id": "{ORG_ID}",
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
