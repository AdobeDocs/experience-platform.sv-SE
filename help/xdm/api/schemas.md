---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;Experience data model;Experience data model;Experience data model;data model;data model;schema register;schema Registry;schema;schema;schema;scheman;scheman;scheman;skapa
solution: Experience Platform
title: API-slutpunkt för scheman
description: Med slutpunkten /schemas i API:t för schemaregister kan du programmässigt hantera XDM-scheman i ditt upplevelseprogram.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# Schemas slutpunkt

Man kan tänka sig ett schema som en plan för de data man vill importera till Adobe Experience Platform. Varje schema består av en klass och noll eller flera schemafältgrupper. The `/schemas` slutpunkt i [!DNL Schema Registry] Med API kan ni programmässigt hantera scheman i ert upplevelseprogram.

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med scheman {#list}

Du kan visa alla scheman under `global` eller `tenant` genom att göra en GET-förfrågan till `/global/schemas` eller `/tenant/schemas`, respektive.

>[!NOTE]
>
>När resurser listas begränsas resultatmängden till 300 objekt. Om du vill returnera resurser som överskrider den här gränsen måste du använda sidindelningsparametrar. Vi rekommenderar också att du använder ytterligare frågeparametrar för att filtrera resultaten och minska antalet returnerade resurser. Se avsnittet om [frågeparametrar](./appendix.md#query) i bilagedokumentet om du vill ha mer information.

**API-format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som innehåller de scheman som du vill hämta: `global` för scheman som skapats av Adobe eller `tenant` för scheman som ägs av din organisation. |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Se [appendix-dokument](./appendix.md#query) för en lista över tillgängliga parametrar. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar en lista med scheman från `tenant` behållare, använda `orderby` frågeparameter för att sortera resultaten efter deras `title` -attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på `Accept` huvud som skickades i begäran. Följande `Accept` rubriker är tillgängliga för listscheman:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar det fullständiga JSON-schemat för varje resurs, med det ursprungliga `$ref` och `allOf` ingår. (Gräns: 300) |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ovannämnda begäran använde `application/vnd.adobe.xed-id+json` `Accept` därför innehåller svaret endast `title`, `$id`, `meta:altId`och `version` attribut för varje schema. Använda den andra `Accept` header (`application/vnd.adobe.xed+json`) returnerar alla attribut för varje schema. Välj lämplig `Accept` sidhuvudet beroende på vilken information du behöver i ditt svar.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Söka efter ett schema {#lookup}

Du kan söka efter ett specifikt schema genom att göra en GET-förfrågan som innehåller schemats ID i sökvägen.

**API-format**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som innehåller det schema som du vill hämta: `global` för ett schema som skapats av Adobe eller `tenant` för ett schema som ägs av din organisation. |
| `{SCHEMA_ID}` | The `meta:altId` eller URL-kodad `$id` av schemat som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar ett schema som anges av dess `meta:altId` i sökvägen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på `Accept` huvud som skickades i begäran. Alla sökförfrågningar kräver en `version` ingår i `Accept` header. Följande `Accept` Det finns rubriker:

| `Accept` header | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw med `$ref` och `allOf`, har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` och `allOf` har åtgärdats, har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw med `$ref` och `allOf`, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` och `allOf` lösta, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` och `allOf` åtgärdade, beskrivningar inkluderades. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` och `allOf` har åtgärdats, har rubriker och beskrivningar. Föråldrade fält indikeras med en `meta:status` attribut för `deprecated`. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om schemat. Vilka fält som returneras beror på `Accept` huvud som skickades i begäran. Experimentera med olika `Accept` rubriker för att jämföra svaren och avgöra vilken rubrik som är bäst för dig.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa ett schema {#create}

Schemadispositionsprocessen börjar med att tilldela en klass. Klassen definierar viktiga beteendeaspekter för data (post- eller tidsserier) samt de minimifält som krävs för att beskriva de data som ska importeras.

>[!NOTE]
>
>Exempelanropet nedan är bara ett grundläggande exempel på hur du skapar ett schema i API:t, med de minimala dispositionskraven för en klass och utan fältgrupper. Fullständiga steg för hur du skapar ett schema i API:t, inklusive hur du tilldelar fält med fältgrupper och datatyper, finns i [självstudiekurs om att skapa scheman](../tutorials/create-schema-api.md).

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Begäran måste innehålla en `allOf` som refererar till `$id` av en klass. Det här attributet definierar den &quot;basklass&quot; som schemat ska implementera. I det här exemplet är basklassen en&quot;Egenskapsinformation&quot;-klass som skapades tidigare.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `allOf` | En array med objekt, där varje objekt refererar till en klass eller fältgrupp vars fält schemat implementerar. Varje objekt innehåller en enda egenskap (`$ref`) vars värde representerar `$id` för den klass eller fältgrupp som det nya schemat kommer att implementera. En klass måste anges, med noll eller flera ytterligare fältgrupper. I ovanstående exempel är det enda objektet i `allOf` är schemats klass. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om det nyligen skapade schemat, inklusive `$id`, `meta:altId`och `version`. Dessa värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Utföra en GET-begäran till [lista alla scheman](#list) i innehavarbehållaren skulle nu inkludera det nya schemat. Du kan göra en [sökbegäran (GET)](#lookup) med URL-kodad `$id` URI för att visa det nya schemat direkt.

Om du vill lägga till fler fält i ett schema kan du utföra en [operationen PATCH](#patch) för att lägga till fältgrupper i schemats `allOf` och `meta:extends` arrayer.

## Uppdatera ett schema {#put}

Du kan ersätta ett helt schema genom en PUT-åtgärd, vilket i själva verket innebär att resursen skrivs om. När du uppdaterar ett schema via en PUT-begäran måste texten innehålla alla fält som krävs när [skapa ett nytt schema](#create) i en POST.

>[!NOTE]
>
>Om du bara vill uppdatera en del av ett schema i stället för att ersätta den helt, se avsnittet om [uppdatera en del av ett schema](#patch).

**API-format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | The `meta:altId` eller URL-kodad `$id` av schemat som du vill skriva om. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran ersätter ett befintligt schema och ändrar dess `title`, `description`och `allOf` attribut.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Svar**

Ett lyckat svar returnerar information om det uppdaterade schemat.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Uppdatera en del av ett schema {#patch}

Du kan uppdatera en del av ett schema genom att använda en PATCH-begäran. The [!DNL Schema Registry] stöder alla vanliga JSON-korrigeringsåtgärder, inklusive `add`, `remove`och `replace`. Mer information om JSON Patch finns i [Grundläggande API-guide](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Om du vill ersätta en hel resurs med nya värden i stället för att uppdatera enskilda fält, se avsnittet om [ersätta ett schema med en PUT-åtgärd](#put).

En av de vanligaste PATCH-åtgärderna är att lägga till tidigare definierade fältgrupper i ett schema, vilket visas i exemplet nedan.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | URL-kodad `$id` URI eller `meta:altId` för det schema som du vill uppdatera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Exempelbegäran nedan lägger till en ny fältgrupp i ett schema genom att lägga till den fältgruppens `$id` värdet till båda `meta:extends` och `allOf` arrayer.

Begärandetexten har formen av en array där varje listat-objekt representerar en specifik ändring i ett enskilt fält. Varje objekt innehåller den åtgärd som ska utföras (`op`), vilket fält åtgärden ska utföras på (`path`) och vilken information som ska ingå i åtgärden (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Svar**

Svaret visar att båda åtgärderna har utförts. Fältgruppen `$id` har lagts till i `meta:extends` array och en referens (`$ref`) till fältgruppen `$id` visas nu i `allOf` array.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Aktivera ett schema för användning i kundprofilen i realtid {#union}

För att ett schema ska kunna delta i [Kundprofil i realtid](../../profile/home.md)måste du lägga till en `union` -tagg till schemats `meta:immutableTags` array. Du kan uppnå detta genom att göra en PATCH-begäran för det aktuella schemat.

>[!IMPORTANT]
>
>Oändringsbara taggar är taggar som ska anges, men aldrig tas bort.

**API-format**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | URL-kodad `$id` URI eller `meta:altId` för det schema som du vill aktivera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Exempelbegäran nedan lägger till en `meta:immutableTags` till ett befintligt schema, vilket ger arrayen ett strängvärde av `union` för att aktivera den för användning i profilen.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Svar**

Ett godkänt svar returnerar informationen om det uppdaterade schemat, vilket visar att `meta:immutableTags` arrayen har lagts till.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

Nu kan du visa unionen för schemats klass för att bekräfta att schemats fält är representerade. Se [slutpunktshandbok för föreningar](./unions.md) för mer information.

## Ta bort ett schema {#delete}

Det kan ibland vara nödvändigt att ta bort ett schema från schemaregistret. Detta görs genom att utföra en DELETE-begäran med det schema-ID som anges i sökvägen.

**API-format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | URL-kodad `$id` URI eller `meta:altId` för det schema som du vill ta bort. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) till schemat. Du måste inkludera en `Accept` huvud i begäran, men bör få HTTP-status 404 (Hittades inte) eftersom schemat har tagits bort från schemaregistret.
