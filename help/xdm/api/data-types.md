---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;Experience data model;data model;data model;data type register;schema Registry;data type;data type;data type;data types;data types;create
solution: Experience Platform
title: API-slutpunkt för datatyper
description: Med slutpunkten /datatypes i API:t för schemaregister kan du programmässigt hantera XDM-datatyper i ditt upplevelseprogram.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Slutpunkt för datatyper

Datatyper används som referenstypfält i klasser eller schemafältgrupper på samma sätt som grundläggande litteralfält, med den största skillnaden är att datatyper kan definiera flera underfält. Även om datatyperna liknar fältgrupper på så sätt att de medger konsekvent användning av en struktur med flera fält, är datatyperna mer flexibla eftersom de kan inkluderas var som helst i schemastrukturen medan fältgrupper bara kan läggas till på rotnivån. Med slutpunkten `/datatypes` i API:t [!DNL Schema Registry] kan du programmässigt hantera datatyper i ditt upplevelseprogram.

>[!NOTE]
>
>Om ett fält definieras som en viss datatyp kan du inte skapa samma fält med en annan datatyp i ett annat schema. Begränsningen gäller för hela organisationens klientorganisation.

## Komma igång

Slutpunkten som används i den här guiden ingår i [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med datatyper {#list}

Du kan lista alla datatyper under behållaren `global` eller `tenant` genom att göra en GET-förfrågan till `/global/datatypes` respektive `/tenant/datatypes`.

>[!NOTE]
>
>När resurser listas begränsas resultatmängden till 300 objekt. Om du vill returnera resurser som överskrider den här gränsen måste du använda sidindelningsparametrar. Vi rekommenderar också att du använder ytterligare frågeparametrar för att filtrera resultaten och minska antalet returnerade resurser. Mer information finns i avsnittet om [frågeparametrar](./appendix.md#query) i bilagan.

**API-format**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som du vill hämta datatyper från: `global` för datatyper som skapats av Adobe eller `tenant` för datatyper som ägs av din organisation. |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. En lista över tillgängliga parametrar finns i [bilagan-dokumentet](./appendix.md#query). |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en lista med datatyper från behållaren `tenant` med hjälp av en `orderby`-frågeparameter för att sortera datatyperna efter deras `title`-attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på det `Accept`-huvud som skickas i begäran. Följande `Accept` rubriker är tillgängliga för att visa datatyper:

| `Accept` huvud | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar den fullständiga JSON-datatypen för varje resurs, med original `$ref` och `allOf` inkluderade. (Gräns: 300) |

{style="table-layout:auto"}

**Svar**

Begäran ovan använde rubriken `application/vnd.adobe.xed-id+json` `Accept`, och därför innehåller svaret bara attributen `title`, `$id`, `meta:altId` och `version` för varje datatyp. Om du använder det andra `Accept`-huvudet (`application/vnd.adobe.xed+json`) returneras alla attribut för varje datatyp. Välj lämpligt `Accept`-huvud beroende på vilken information du behöver i ditt svar.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
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
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Söka efter en datatyp {#lookup}

Du kan söka efter en viss datatyp genom att ta med datatypens ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som innehåller den datatyp som du vill hämta: `global` för en datatyp som skapats av Adobe eller `tenant` för en datatyp som ägs av din organisation. |
| `{DATA_TYPE_ID}` | `meta:altId` eller URL-kodad `$id` för den datatyp som du vill söka efter. |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar en datatyp med dess `meta:altId`-värde som anges i sökvägen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på det `Accept`-huvud som skickas i begäran. Alla uppslagsbegäranden kräver att `version` inkluderas i rubriken `Accept`. Följande `Accept` rubriker är tillgängliga:

| `Accept` huvud | Beskrivning |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw med `$ref` och `allOf` har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` och `allOf` har matchats, har rubriker och beskrivningar. |
| `application/vnd.adobe.xed-notext+json; version=1` | Raw med `$ref` och `allOf`, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` och `allOf` har matchats, inga titlar eller beskrivningar. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` och `allOf` löstes, beskrivningar inkluderades. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar informationen om datatypen. Vilka fält som returneras beror på det `Accept`-huvud som skickas i begäran. Experimentera med olika `Accept`-huvuden för att jämföra svaren och avgöra vilken rubrik som är bäst för ditt användningsfall.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Skapa en datatyp {#create}

Du kan definiera en anpassad datatyp under behållaren `tenant` genom att göra en POST-förfrågan.

**API-format**

```http
POST /tenant/datatypes
```

**Begäran**

Till skillnad från fältgrupper, kräver inte `meta:extends`- eller `meta:intendedToExtend`-fält för att definiera en datatyp, och inte heller måste fält kapslas för att undvika kollisioner.

När det gäller att definiera fältstrukturen för själva datatypen kan du använda primitiva typer (som `string` eller `object`) eller referera till andra befintliga datatyper via `$ref`-attribut. Mer information om det förväntade formatet för olika XDM-fälttyper finns i guiden [Definiera anpassade XDM-fält i API](../tutorials/custom-fields-api.md).

I följande begäran skapas en egenskapskonstruktion-objekttyp med underegenskaperna `yearBuilt`, `propertyType` och `location`:

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om den nya datatypen, inklusive `$id`, `meta:altId` och `version`. Dessa tre värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Om du utför en GET-begäran om att [visa alla datatyper](#list) i klientbehållaren skulle det nu inkludera datatypen Egenskapsinformation. Du kan också [utföra en sökning (GET) ](#lookup) med URL-kodad `$id` URI för att visa den nya datatypen direkt.

## Uppdatera en datatyp {#put}

Du kan ersätta en hel datatyp genom en PUT-åtgärd, vilket i själva verket innebär att resursen skrivs om. När du uppdaterar en datatyp via en PUT-begäran måste brödtexten innehålla alla fält som krävs när [en ny datatyp ](#create) skapas i en POST-begäran.

>[!NOTE]
>
>Om du bara vill uppdatera en del av en datatyp i stället för att ersätta den helt, ska du läsa avsnittet [Uppdatera en del av en datatyp](#patch).

**API-format**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATA_TYPE_ID}` | `meta:altId` eller URL-kodad `$id` för den datatyp som du vill skriva om. |

{style="table-layout:auto"}

**Begäran**

Följande begäran skriver om en befintlig datatyp och lägger till ett nytt `floorSize`-fält.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Svar**

Ett godkänt svar returnerar information om den uppdaterade datatypen.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Uppdatera en del av en datatyp {#patch}

Du kan uppdatera en del av en datatyp genom att använda en PATCH-begäran. [!DNL Schema Registry] stöder alla JSON-standardåtgärder för korrigering, inklusive `add`, `remove` och `replace`. Mer information om JSON Patch finns i guiden [Grundläggande API](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Om du vill ersätta en hel resurs med nya värden i stället för att uppdatera enskilda fält läser du avsnittet [Ersätta en datatyp med en PUT-åtgärd](#put).

**API-format**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATA_TYPE_ID}` | URL-kodad `$id` URI eller `meta:altId` för den datatyp som du vill uppdatera. |

{style="table-layout:auto"}

**Begäran**

Exempelbegäran nedan uppdaterar `description` för en befintlig datatyp och lägger till ett nytt `floorSize`-fält.

Begärandetexten har formen av en array där varje listat-objekt representerar en specifik ändring i ett enskilt fält. Varje objekt innehåller åtgärden som ska utföras (`op`), vilket fält åtgärden ska utföras på (`path`) och vilken information som ska inkluderas i åtgärden (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Svar**

Svaret visar att båda åtgärderna utfördes utan fel. `description` har uppdaterats och `floorSize` har lagts till under `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Ta bort en datatyp {#delete}

Det kan ibland vara nödvändigt att ta bort en datatyp från schemaregistret. Detta görs genom att utföra en DELETE-begäran med det datatyp-ID som anges i sökvägen.

**API-format**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATA_TYPE_ID}` | URL-kodad `$id` URI eller `meta:altId` för den datatyp som du vill ta bort. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en [sökbegäran (GET)](#lookup) till datatypen. Du måste inkludera ett `Accept`-huvud i begäran, men du bör få HTTP-status 404 (Hittades inte) eftersom datatypen har tagits bort från schemaregistret.
