---
title: API-slutpunkt för beräknade attribut
description: Lär dig hur du skapar, visar, uppdaterar och tar bort beräknade attribut med Real-Time Customer Profile API.
source-git-commit: e1c7d097f7ab39d05674c3dad620bea29f08092b
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 0%

---


# API-slutpunkt för beräknade attribut

>[!IMPORTANT]
>
>Åtkomsten till API:t är begränsad. Kontakta Adobe Support om du vill veta hur du får åtkomst till API:t för beräknade attribut.

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering. Den här guiden innehåller exempel på API-anrop för att utföra grundläggande CRUD-åtgärder med `/attributes` slutpunkt.

Om du vill veta mer om beräknade attribut börjar du med att läsa [översikt över beräknade attribut](overview.md).

## Komma igång

API-slutpunkten som används i den här guiden är en del av [Kundprofil-API i realtid](https://www.adobe.com/go/profile-apis-en).

Innan du fortsätter bör du granska [Starthandbok för att komma igång med profil-API](../api/getting-started.md) för länkar till rekommenderad dokumentation, en guide till hur du läser de exempel-API-anrop som visas i det här dokumentet samt viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

Läs även dokumentationen för följande tjänst:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Guiden Komma igång med schemaregister](../../xdm/api/getting-started.md#know-your-tenant_id): Information om `{TENANT_ID}`, som visas i svaren i hela den här handboken, tillhandahålls.

## Hämta en lista med beräknade attribut {#list}

Du kan hämta en lista över alla beräknade attribut för din organisation genom att göra en GET-förfrågan till `/attributes` slutpunkt.

**API-format**

The `/attributes` slutpunkten har stöd för flera frågeparametrar som hjälper dig att filtrera dina resultat. Även om dessa parametrar är valfria rekommenderar vi starkt att de används för att minska dyra overheadkostnader när du listar resurser. Om du anropar den här slutpunkten utan parametrar hämtas alla beräknade attribut som är tillgängliga för din organisation. Flera parametrar kan inkluderas, avgränsade med et-tecken (`&`).

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

Följande frågeparametrar kan användas när en lista med beräknade attribut hämtas:

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `limit` | En parameter som anger det maximala antalet objekt som returneras som en del av svaret. Det minsta värdet för den här parametern är 1 och det högsta värdet är 40. Om den här parametern inte ingår returneras som standard 20 objekt. | `limit=20` |
| `offset` | En parameter som anger antalet objekt som ska hoppas över innan objekten returneras. | `offset=5` |
| `sortBy` | En parameter som anger i vilken ordning de returnerade objekten sorteras. Tillgängliga alternativ inkluderar `name`, `status`, `updateEpoch`och `createEpoch`. Du kan också välja om du vill sortera i stigande eller fallande ordning genom att inte inkludera eller inkludera en `-` framför sorteringsalternativet. Som standard sorteras objekten efter `updateEpoch` i fallande ordning. | `sortBy=name` |
| `property` | En parameter som gör att du kan filtrera på olika beräknade attributfält. Egenskaper som stöds är bland annat `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch`och `status`. Vilka åtgärder som stöds beror på vilken egenskap som visas. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (!=contains()</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Begäran**

Följande begäran hämtar de tre senaste beräknade attributen som uppdaterades i din organisation.

+++ En exempelbegäran om att hämta en lista med beräknade attribut.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med en lista över de tre senaste uppdaterade beräknade attributen som tillhör din organisation och sandlåda.

+++ Ett exempelsvar för att hämta en lista med beräknade attribut.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `_links` | Ett objekt som innehåller den sidnumreringsinformation som krävs för att komma åt den sista resultatsidan, nästa resultatsida, föregående resultatsida eller den aktuella resultatsidan. |
| `computedAttributes` | En array som innehåller de beräknade attributen baserat på dina frågeparametrar. Mer information om den beräknade attributarrayen finns i [hämta ett visst beräknat attributavsnitt](#get). |
| `_page` | Ett objekt som innehåller metadata om de returnerade resultaten. Detta inkluderar information om aktuell förskjutning, antalet returnerade beräknade attribut, det totala antalet beräknade attribut samt gränsen för returnerade beräknade attribut. |

+++

## Skapa ett beräknat attribut {#create}

Om du vill skapa ett beräknat attribut börjar du med att göra en POST-förfrågan till `/attributes` slutpunkt med en begärandebrödtext som innehåller information om det beräknade attributet som du vill skapa.

**API-format**

```http
POST /attributes
```

**Begäran**

+++ En exempelbegäran om att skapa ett nytt beräknat attribut.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `name` | Namnet på det beräknade attributfältet, som en sträng. Namnet på det beräknade attributet får endast bestå av alfanumeriska tecken utan mellanslag eller understreck. Detta värde **måste** vara unik bland alla beräknade attribut. Det här namnet bör vara en cameraCase-version av `displayName`. |
| `description` | En beskrivning av det beräknade attributet. Detta är särskilt användbart när flera beräknade attribut har definierats, eftersom det kommer att hjälpa andra inom organisationen att fastställa rätt beräknat attribut att använda. |
| `displayName` | Det beräknade attributets visningsnamn. Det här namnet visas när du anger dina beräknade attribut i Adobe Experience Platform-gränssnittet. |
| `expression` | Ett objekt som representerar frågeuttrycket för det beräknade attribut som du försöker skapa. |
| `expression.type` | Uttryckets typ. För närvarande stöds bara PQL. |
| `expression.format` | Uttryckets format. För närvarande, endast `pql/text` stöds. |
| `expression.value` | Uttryckets värde. |
| `keepCurrent` | Ett booleskt värde som avgör om det beräknade attributets värde uppdateras eller inte med hjälp av snabb uppdatering. För närvarande ska det här värdet anges till `false`. |
| `duration` | Ett objekt som representerar uppslagsperioden för det beräknade attributet. Uppslagsperioden representerar hur långt tillbaka som kan slås tillbaka för att beräkna det beräknade attributet. |
| `duration.count` | Ett tal som representerar längden för uppslagsperioden. Möjliga värden beror på värdet på `duration.unit` fält. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | En sträng som representerar den tidsenhet som ska användas för uppslagsperioden. Möjliga värden är: `HOURS`, `DAYS`, `WEEKS`och `MONTHS`. |
| `status` | Status för beräknat attribut. Möjliga värden är `DRAFT` och `NEW`. |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om det nya beräknade attributet.

+++ Ett samplingssvar när ett nytt beräknat attribut skapas.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Det systemgenererade ID:t för det nya beräknade attributet. |
| `status` | Det beräknade attributets status. Detta kan antingen vara `DRAFT` eller `NEW`. |
| `createEpoch` | Tiden då det beräknade attributet skapades, i sekunder. |
| `updateEpoch` | Den tidpunkt då det beräknade attributet senast uppdaterades, i sekunder. |
| `createdBy` | ID för den användare som skapade det beräknade attributet. |

+++

## Hämta ett specifikt beräknat attribut {#get}

Du kan hämta detaljerad information om ett specifikt beräknat attribut genom att göra en GET-förfrågan till `/attributes` slutpunkt och ange ID:t för det beräknade attribut som du vill hämta i sökvägen för begäran.

**API-format**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Begäran**

+++ En exempelbegäran om att hämta ett specifikt beräknat attribut.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om det angivna beräknade attributet.

+++ Ett samplingssvar när ett visst beräknat attribut hämtas.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Ett unikt, skrivskyddat, systemgenererat ID som kan användas för att referera till det beräknade attributet under andra API-åtgärder. |
| `type` | En sträng som visar att det returnerade objektet är ett beräknat attribut. |
| `name` | Namnet på det beräknade attributet. |
| `displayName` | Det beräknade attributets visningsnamn. Det här namnet visas när du anger dina beräknade attribut i Adobe Experience Platform-gränssnittet. |
| `description` | En beskrivning av det beräknade attributet. Detta är särskilt användbart när flera beräknade attribut har definierats, eftersom det kommer att hjälpa andra inom organisationen att fastställa rätt beräknat attribut att använda. |
| `imsOrgId` | ID:t för organisationen som det beräknade attributet tillhör. |
| `sandbox` | Sandlådeobjektet innehåller information om den sandlåda som det beräknade attributet konfigurerades i. Den här informationen hämtas från sandlådehuvudet som skickas i begäran. Mer information finns i [översikt över sandlådor](../../sandboxes/home.md). |
| `path` | The `path` till det beräknade attributet. |
| `keepCurrent` | Ett booleskt värde som avgör om det beräknade attributets värde uppdateras eller inte med hjälp av snabb uppdatering. |
| `expression` | Ett objekt som innehåller attributets uttryck. |
| `mergeFunction` | Ett objekt som innehåller kopplingsfunktionen för det beräknade attributet. Det här värdet baseras på motsvarande aggregeringsparameter i det beräknade attributets uttryck. Möjliga värden är `SUM`, `MIN`, `MAX`och `MOST_RECENT`. |
| `status` | Det beräknade attributets status. Detta kan vara något av följande värden: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED`, eller `DISABLED`. |
| `schema` | Ett objekt som innehåller information om schemat där uttrycket utvärderas i. För närvarande, endast `_xdm.context.profile` stöds. |
| `lastEvaluationTs` | En tidsstämpel som representerar när det beräknade attributet senast utvärderades. |
| `createEpoch` | Tiden då det beräknade attributet skapades, i sekunder. |
| `updateEpoch` | Den tidpunkt då det beräknade attributet senast uppdaterades, i sekunder. |
| `createdBy` | ID för den användare som skapade det beräknade attributet. |

+++

## Ta bort ett visst beräknat attribut {#delete}

Du kan ta bort ett visst beräknat attribut genom att göra en DELETE-begäran till `/attributes` slutpunkt och ange ID:t för det beräknade attribut som du vill ta bort i sökvägen för begäran.

>[!IMPORTANT]
>
>Begäran om borttagning kan bara användas för att ta bort beräknade attribut med statusen **utkast** (`DRAFT`). Den här slutpunkten **inte** används för att ta bort beräknade attribut i något annat läge.

**API-format**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | The `id` värdet på det beräknade attributet som du vill ta bort. |

**Begäran**

+++ En exempelbegäran om att ta bort ett beräknat attribut.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 202 med information om det borttagna beräknade attributet.

+++ Ett exempelsvar när ett beräknat attribut tas bort.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Uppdatera ett specifikt beräknat attribut

Du kan uppdatera ett specifikt beräknat attribut genom att göra en PATCH-begäran till `/attributes` slutpunkt och ange ID:t för det beräknade attribut som du vill uppdatera i sökvägen för begäran.

>[!IMPORTANT]
>
>När du uppdaterar ett beräknat attribut kan endast följande fält uppdateras:
>
>- Om aktuell status är `NEW`kan statusen bara ändras till `DISABLED`.
>- Om aktuell status är `DRAFT`kan du ändra värdena för följande fält: `name`, `description`, `keepCurrent`, `expression`och `duration`. Du kan också ändra status från `DRAFT` till `NEW`. Ändringar i systemgenererade fält, till exempel `mergeFunction` eller `path` returnerar ett fel.
>- Om aktuell status är antingen `PROCESSING` eller `PROCESSED`kan statusen bara ändras till `DISABLED`.

**API-format**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | The `id` värdet på det beräknade attributet som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar statusen för det beräknade attributet från `DRAFT` till `NEW`.

+++ En exempelbegäran om att uppdatera ett beräknat attribut.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om ditt nyligen uppdaterade beräknade attribut.

+++ Ett exempelsvar när ett beräknat attribut uppdateras.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Nästa steg

Nu när du har lärt dig grunderna i beräknade attribut kan du börja definiera dem för din organisation. Om du vill veta hur du använder beräknade attribut i användargränssnittet för Experience Platform kan du läsa [gränssnittshandbok för beräknade attribut](./ui.md).
