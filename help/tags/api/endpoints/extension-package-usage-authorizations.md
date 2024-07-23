---
title: Slutpunkt för användningsauktorisering för tilläggspaket
description: Lär dig hur du anropar slutpunkten för /extension_package_usage-auktoriseringar i Reactor API.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# Slutpunkt för användningsauktorisering för tilläggspaket

Ett tilläggspaket representerar ett [tillägg](./extensions.md) som har skapats av en tilläggsutvecklare. Ytterligare funktioner som kan göras tillgängliga för tagganvändare definieras av ett tilläggspaket. Dessa funktioner kan omfatta huvudmoduler och delade moduler, men tillhandahålls oftast som [regelkomponenter](./rule-components.md) (händelser, villkor och åtgärder) och [dataelement](./data-elements.md).

Ett tilläggspaket ägs av utvecklarens [företag](./companies.md). Ägare till tilläggspaket kan auktorisera andra företag att använda sina privata versioner av paketen. Varje auktoriserat företag får en användarbehörighet för ett enda tilläggspaket som är giltigt för alla framtida och aktuella privata versioner av paketet.

## Komma igång

Slutpunkten som används i den här guiden ingår i [Reaktors-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Innan du fortsätter bör du läsa [kom igång-guiden](../getting-started.md) för att få viktig information om hur du autentiserar dig för API:t.

## Hämta användningstillstånd för tilläggspaket för ett tilläggspaket {#list}

Om du vill hämta en lista över användningsauktoriseringar för ett tilläggspaket ska du göra en GET-begäran till följande slutpunkt.

**API-format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beskrivning |
| --- | --- |
| `{PROPERTY_ID}` | `ID` för egenskapen vars användningsbehörighet för tilläggspaketet du vill visa. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med tilläggspaket.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
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

## Skapa en användningsbehörighet för tilläggspaket {#create}

Skapa en användningsbehörighet för tilläggspaket för varje [tilläggspaket](./extension-packages.md) och `{ORG_ID}` i organisationen som du vill auktorisera. Om du vill skapa en ny användningsbehörighet för tilläggspaket skickar du en POST till slutpunkten nedan.

**API-format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beskrivning |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` för tilläggspaketet som du vill skapa en auktorisering för.&quot; |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes.authorized_org_id` | `ID` för organisationen som du vill auktorisera. |

**Svar**

Ett godkänt svar returnerar information om användningsauktoriseringen för det nya tilläggspaketet.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>I exempelsvaret ovan är auktoriseringen för närvarande i `pending_approval`-steget. Organisationen måste godkänna behörigheten innan tilläggspaketet används. Organisationens användare kan bläddra i det privata tilläggspaketet medan auktoriseringen väntar på godkännande, men de kan inte installera det och kan inte hitta det i sin tilläggskatalog.

## Hämta en lista över användningstillstånd för tilläggspaket {#list-authorizations}

Du kan hämta en lista över användningsauktoriseringar för tilläggspaket genom att göra en GET-begäran.

**API-format**

```http
GET /extension_package_usage_authorizations
```

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett godkänt svar returnerar en lista med tilläggspaket.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Ta bort en användningsbehörighet för tilläggspaket {#delete}

Om du vill ta bort en användningsbehörighet för tilläggspaket tar du med `ID` i sökvägen till en DELETE-begäran. Detta förhindrar att den auktoriserade organisationen kan visa de privata versionerna av tilläggspaketet i katalogen och inte installera det på sina egenskaper.

>[!NOTE]
>
>Tidigare installerade privata versioner fortsätter att fungera som förväntat.

**API-format**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `ID` | `ID` för den användningsbehörighet för tilläggspaketet som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) utan svarstext. Detta anger att tillägget har tagits bort.

## Uppdatera användningsbehörighet för tilläggspaket {#update}

Om du vill godkänna eller avvisa en användningsbehörighet för tilläggspaket tar du med `ID` i sökvägen till en PATCH-begäran.

>[!NOTE]
>
>Om du vill godkänna eller avvisa en användningsbehörighet för tilläggspaket för ditt företag måste du ha `manage_properties` rättigheter.

**API-format**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `ID` | `ID` för den användningsbehörighet för tilläggspaketet som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Egenskap | Beskrivning |
| --- | --- |
| `attributes` | De attribut som du vill ändra. För användningsauktoriseringar för tilläggspaket kan du revidera deras `state`. |

**Svar**

Ett godkänt svar returnerar information om den ändrade behörigheten för användning av tilläggspaket.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>När auktoriseringen har godkänts kan din organisation installera tilläggspaketet på dina egenskaper.

## Hämta data för tilläggspaketet för en användningsbehörighet för tilläggspaket {#retrieve-data}

Du kan hämta data för tilläggspaketet för en åtkomstpaketets användningsbehörighet genom att göra en GET-begäran.

**API-format**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parameter | Beskrivning |
| --- | --- |
| `ID` | `ID` för den användningsbehörighet för tilläggspaketet som du vill hämta. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Svar**

Ett lyckat svar returnerar data för tilläggspaketet för en auktorisering av tilläggspaket.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
