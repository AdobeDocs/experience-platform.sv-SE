---
keywords: Experience Platform;hem;populära ämnen;api;Attributbaserad åtkomstkontroll;attributbaserad åtkomstkontroll
solution: Experience Platform
title: API-slutpunkt för produkter
description: Med slutpunkten /products i API:t för attributbaserad åtkomstkontroll kan du programmässigt hantera produkter i Adobe Experience Platform.
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Slutpunkt för produkter

The `/products` -slutpunkten i det attributbaserade API:t för åtkomstkontroll gör det möjligt att programmässigt hantera produkter samt behörighetskategorier och behörighetsgrupper som är kopplade till produkter i organisationen.

## Komma igång

API-slutpunkten som används i den här guiden är en del av det attributbaserade API:t för åtkomstkontroll. Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista över berättigade produkter {#list}

Du kan hämta en lista över berättigade produkter genom att göra en GET-förfrågan till `/products` slutpunkt.

**API-format**

```http
GET /products/
```

**Begäran**

Följande begäran hämtar en lista över berättigade produkter som tillhör din organisation.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar en lista över berättigade produkter som tillhör din organisation.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Motsvarande ID för den efterfrågade produkten. |
| `name` | Namnet på den efterfrågade produkten. |
| `serviceCode` | Motsvarande servicekod för den efterfrågade produkten. |

## Sök behörighetskategorier efter produkt-ID

Du kan slå upp behörighetskategorier för en viss produkt genom att göra en GET-förfrågan till `/products/{PRODUCT_ID}/categories` slutpunkt när du anger produkt-id:t.

**API-format**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parameter | Beskrivning |
| --- | --- |
| {PRODUCT_ID} | ID:t för den produkt som är associerad med de behörighetskategorier som du vill söka efter. |

**Begäran**

Följande begäran hämtar behörighetskategorier som är associerade med `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar de behörighetskategorier som är associerade med det produkt-ID du har frågat.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `category` | Behörighetskategorierna som är tillgängliga inom det efterfrågade produkt-ID:t. |
| `name` | Namnet på behörighetskategorin. |

## Söka efter behörighetsgrupper efter produkt-ID

Du kan söka efter behörighetsgrupper för en viss produkt genom att göra en GET-förfrågan till `/products/{PRODUCT_ID}/permission-sets` slutpunkt när du anger produkt-id:t.

**API-format**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parameter | Beskrivning |
| --- | --- |
| {PRODUCT_ID} | ID:t för den produkt som är associerad med de behörighetsgrupper som du vill söka efter. |

**Begäran**

Följande begäran hämtar behörighetsgrupper som är associerade med `{PRODUCT_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Svar**

Ett godkänt svar returnerar de behörighetsgrupper som är kopplade till det produkt-ID du frågade.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `permission-sets` | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| `id` | Motsvarande ID för den efterfrågade behörighetsgruppen. |
| `name` | Motsvarande namn för den efterfrågade behörighetsgruppen. |
| `category` | Den tillgängliga behörighetskategorin. |
| `permissions` | Behörigheter omfattar möjligheten att visa och/eller använda plattformsfunktioner, som att skapa sandlådor, definiera scheman och hantera datauppsättningar. |
| `permissions.resource` | Den tillgång eller det objekt som ett ämne kan eller inte kan komma åt. Resurser kan vara filer, program, servrar eller till och med API:er. |
| `permissions.actions` | Den åtgärd som ett ämne tillåts att göra mot en frågad resurs. Möjliga värden är: `view`, `read`, `create`, `edit`och `delete` |
