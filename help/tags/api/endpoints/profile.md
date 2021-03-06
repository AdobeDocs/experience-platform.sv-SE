---
title: Profilslutpunkt
description: Lär dig hur du anropar slutpunkten /profiles i Reaktors API.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Profilslutpunkt

I Reactor API representerar en profil en Adobe Experience Platform-användare. Reaktors-API:t underhåller inte sin egen databas med användare och behörigheter, utan bygger i stället på Adobe-ID:n som hanteras av [Adobe system för identitetshantering (IMS)](https://helpx.adobe.com/enterprise/using/identity.html).

En profil innehåller all information om den inloggade användaren, inklusive alla IMS-organisationer de tillhör, de produktprofiler de tillhör inom varje organisation och de rättigheter de har från varje produktprofil.

## Komma igång

Slutpunkten som används i den här guiden är en del av [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Läs igenom [komma igång-guide](../getting-started.md) om du vill ha viktig information om hur du autentiserar till API:t.

## Hämta den aktuella profilen {#lookup}

Du kan hämta information om den inloggade profilen genom att göra en GET-förfrågan till `/profile` slutpunkt.

**API-format**

```http
GET /profile
```

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar informationen om profilen.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```
