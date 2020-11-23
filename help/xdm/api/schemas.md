---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Skapa ett schema
description: Med slutpunkten /schemas i API:t för schemaregister kan du programmässigt hantera XDM-scheman i ditt upplevelseprogram.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---


# Schemas slutpunkt

Man kan tänka sig ett schema som en plan för de data man vill importera till Adobe Experience Platform. Varje schema består av en klass och noll eller flera mixiner. Med `/schemas` slutpunkten i [!DNL Schema Registry] API kan du programmässigt hantera scheman i ditt upplevelseprogram.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Innan du fortsätter bör du läsa [Komma igång-guiden](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med scheman {#list}

Du kan visa alla scheman under `global` - eller `tenant` behållaren genom att göra en GET-förfrågan till `/global/schemas` respektive `/tenant/schemas`.

>[!NOTE]
>
>När resurser listas begränsas resultatmängden till 300 objekt. Om du vill returnera resurser som överskrider den här gränsen måste du använda sidindelningsparametrar. Vi rekommenderar också att du använder ytterligare frågeparametrar för att filtrera resultaten och minska antalet returnerade resurser. Mer information finns i avsnittet om [frågeparametrar](./appendix.md#query) i bilagan.

**API-format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som innehåller de scheman som du vill hämta: `global` för scheman som skapats av Adobe eller `tenant` för scheman som ägs av din organisation. |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. En lista med tillgängliga parametrar finns i [bilagan](./appendix.md#query) . |

**Begäran**

Följande begäran hämtar en lista med scheman från `tenant` behållaren och använder en `orderby` frågeparameter för att sortera resultaten efter deras `title` attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på vilket sidhuvud som skickas i begäran `Accept` . Följande `Accept` rubriker är tillgängliga för listscheman:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar det fullständiga JSON-schemat för varje resurs, med ursprungligt `$ref` och `allOf` inkluderat. (Gräns: 300) |

**Svar**

I begäran ovan användes `application/vnd.adobe.xed-id+json``Accept` rubriken, vilket innebär att svaret endast innehåller attributen `title`, `$id`, `meta:altId`och `version` för varje schema. Om du använder den andra `Accept` rubriken (`application/vnd.adobe.xed+json`) returneras alla attribut för varje schema. Välj lämplig `Accept` rubrik beroende på vilken information du behöver i ditt svar.

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
| `{SCHEMA_ID}` | Den `meta:altId` eller URL-kodade `$id` för schemat som du vill söka efter. |

**Begäran**

Följande begäran hämtar ett schema som anges av dess `meta:altId` värde i sökvägen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på vilket sidhuvud som skickas i begäran `Accept` . Alla uppslagsbegäranden måste `version` inkluderas i `Accept` rubriken. The following `Accept` headers are available:

| `Accept` header | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw med `$ref` och `allOf`har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` och `allOf` är åtgärdade, har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw med `$ref` och `allOf`, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` och `allOf` löste sig - inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` och `allOf` åtgärdade, beskrivningar inkluderades. |

**Svar**

Ett lyckat svar returnerar information om schemat. Vilka fält som returneras beror på vilket sidhuvud som skickas i begäran `Accept` . Experimentera med olika `Accept` rubriker för att jämföra svaren och ta reda på vilket sidhuvud som är bäst för dig.

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
  "imsOrg": "{IMS_ORG}",
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
>Exempelanropet nedan är bara ett grundläggande exempel på hur du skapar ett schema i API:t, med de minimala dispositionskraven för en klass och inga mixins. Fullständiga steg för hur du skapar ett schema i API:t, inklusive hur du tilldelar fält med mixiner och datatyper, finns i självstudiekursen [för att skapa](../tutorials/create-schema-api.md)schema.

**API-format**

```http
POST /tenant/schemas
```

**Begäran**

Begäran måste innehålla ett `allOf` attribut som refererar till `$id` en klass. Det här attributet definierar den &quot;basklass&quot; som schemat ska implementera. I det här exemplet är basklassen en&quot;Egenskapsinformation&quot;-klass som skapades tidigare.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `allOf` | En array med objekt, där varje objekt refererar till en klass eller blandning vars fält schemat implementerar. Varje objekt innehåller en enda egenskap (`$ref`) vars värde motsvarar `$id` klassens eller mixens värde, vilket innebär att det nya schemat implementeras. En klass måste anges, med noll eller flera ytterligare blandningar. I exemplet ovan är det enda objektet i arrayen `allOf` schemaklassen. |

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
    "imsOrg": "{IMS_ORG}",
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

Om en begäran om GET om att [lista alla scheman](#list) i innehavarbehållaren skulle utföras, skulle det nya schemat nu ingå. Du kan utföra en [sökbegäran](#lookup) (GET) med den URL-kodade `$id` URI:n för att visa det nya schemat direkt.

Om du vill lägga till fler fält i ett schema kan du utföra en [PATCH-åtgärd](#patch) för att lägga till blandningar i schemats `allOf` - och `meta:extends` -arrayer.

## Uppdatera ett schema {#put}

Du kan ersätta ett helt schema genom en PUT-åtgärd, vilket i själva verket innebär att resursen skrivs om. När du uppdaterar ett schema via en PUT-begäran måste texten innehålla alla fält som krävs när du [skapar ett nytt schema](#create) i en POST-begäran.

>[!NOTE]
>
>Om du bara vill uppdatera en del av ett schema i stället för att ersätta den helt, ska du läsa avsnittet om att [uppdatera en del av ett schema](#patch).

**API-format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den `meta:altId` eller URL-kodade `$id` för schemat som du vill skriva om. |

**Begäran**

Följande begäran ersätter ett befintligt schema och ändrar dess `title`-, `description`och `allOf` -attribut.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Du kan uppdatera en del av ett schema genom att använda en PATCH-begäran. Den [!DNL Schema Registry] stöder alla vanliga JSON Patch-åtgärder, inklusive `add`, `remove`och `replace`. Mer information om JSON Patch finns i [API-handboken](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Om du vill ersätta en hel resurs med nya värden i stället för att uppdatera enskilda fält läser du avsnittet om att [ersätta ett schema med en PUT-åtgärd](#put).

En av de vanligaste PATCH-åtgärderna är att lägga till tidigare definierade blandningar i ett schema, vilket visas i exemplet nedan.

**API-format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` det schema som du vill uppdatera. |

**Begäran**

Exempelbegäran nedan lägger till en ny blandning i ett schema genom att lägga till den mixins `$id` värde till både `meta:extends` - och `allOf` -arrayerna.

Begärandetexten har formen av en array där varje listat-objekt representerar en specifik ändring i ett enskilt fält. Varje objekt innehåller den åtgärd som ska utföras (`op`), vilket fält åtgärden ska utföras på (`path`) och vilken information som ska inkluderas i åtgärden (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Svaret visar att båda åtgärderna har utförts. Mixin `$id` har lagts till i `meta:extends` arrayen och en referens (`$ref`) till mixin `$id` visas nu i `allOf` arrayen.

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
    "imsOrg": "{IMS_ORG}",
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

För att ett schema ska kunna ingå i kundprofilen [i](../../profile/home.md)realtid måste du lägga till en `union` tagg i schemats `meta:immutableTags` matris. Du kan uppnå detta genom att göra en PATCH-begäran för det aktuella schemat.

>[!IMPORTANT]
>
>Oändringsbara taggar är taggar som ska anges, men aldrig tas bort.

**API-format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` det schema som du vill aktivera. |

**Begäran**

Exempelbegäran nedan lägger till en `meta:immutableTags` array i ett befintligt schema, vilket ger arrayen ett strängvärde på `union` för att den ska kunna användas i profilen.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Ett lyckat svar returnerar informationen om det uppdaterade schemat, vilket visar att `meta:immutableTags` arrayen har lagts till.

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
    "imsOrg": "{IMS_ORG}",
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

Nu kan du visa unionen för schemats klass för att bekräfta att schemats fält är representerade. Mer information finns i slutpunktshandboken för [fackföreningar](./unions.md) .

## Ta bort ett schema {#delete}

Det kan ibland vara nödvändigt att ta bort ett schema från schemaregistret. Detta görs genom att utföra en DELETE-begäran med det schema-ID som anges i sökvägen.

**API-format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{SCHEMA_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` det schema som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) till schemat. Du måste inkludera en rubrik i begäran, men du bör få HTTP-status 404 (Hittades inte) eftersom schemat har tagits bort från schemaregistret. `Accept`