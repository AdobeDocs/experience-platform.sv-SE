---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;Experience data model;experience data model;data model;data model;class register;schema Registry;class;class;classes;classes;create
solution: Experience Platform
title: API-slutpunkt för klasser
description: Med slutpunkten /classes i API:t för schemaregister kan du programmässigt hantera XDM-klasser i ditt upplevelseprogram.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# Klassslutpunkt

Alla XDM-scheman (Experience Data Model) måste baseras på en klass. En klass avgör den grundläggande strukturen för gemensamma egenskaper som alla scheman baserade på den klassen måste innehålla, samt vilka schemafältgrupper som kan användas i dessa scheman. Dessutom avgör en schemaklass vilka beteendeaspekter av data som ett schema innehåller, varav det finns två typer:

* **[!UICONTROL Record]**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **[!UICONTROL Time-series]**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

>[!NOTE]
>
>Mer information om klasser för databeteenden i termer av hur de påverkar schemakomposition finns i [grunderna för schemakomposition](../schema/composition.md).

The `/classes` slutpunkt i [!DNL Schema Registry] Med API kan ni programmässigt hantera klasser i ert upplevelseprogram.

## Komma igång

Slutpunkten som används i den här guiden är en del av [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Läs igenom [komma igång-guide](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Hämta en lista med klasser {#list}

Du kan visa alla klasser under `global` eller `tenant` genom att göra en GET-förfrågan till `/global/classes` eller `/tenant/classes`, respektive.

>[!NOTE]
>
>När resurser listas begränsas resultatmängden till 300 objekt. Om du vill returnera resurser som överskrider den här gränsen måste du använda sidindelningsparametrar. Vi rekommenderar också att du använder ytterligare frågeparametrar för att filtrera resultaten och minska antalet returnerade resurser. Se avsnittet om [frågeparametrar](./appendix.md#query) i bilagedokumentet om du vill ha mer information.

**API-format**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Behållaren som du vill hämta klasser från: `global` för klasser som skapats av Adobe eller `tenant` för lektioner som ägs av din organisation. |
| `{QUERY_PARAMS}` | Valfria frågeparametrar för att filtrera resultat efter. Se [appendix-dokument](./appendix.md#query) för en lista över tillgängliga parametrar. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar en lista över klasser från `tenant` behållare, använda `orderby` frågeparameter för att sortera klasserna efter deras `title` -attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Svarsformatet beror på `Accept` huvud som skickades i begäran. Följande `Accept` rubriker är tillgängliga för klasser:

| `Accept` header | Beskrivning |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Returnerar en kort sammanfattning av varje resurs. Det här är det rekommenderade huvudet för att lista resurser. (Gräns: 300) |
| `application/vnd.adobe.xed+json` | Returnerar en fullständig JSON-klass för varje resurs, med ursprunglig `$ref` och `allOf` ingår. (Gräns: 300) |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ovannämnda begäran använde `application/vnd.adobe.xed-id+json` `Accept` därför innehåller svaret endast `title`, `$id`, `meta:altId`och `version` attribut för varje klass. Använda den andra `Accept` header (`application/vnd.adobe.xed+json`) returnerar alla attribut för varje klass. Välj lämplig `Accept` sidhuvudet beroende på vilken information du behöver i ditt svar.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Söka efter en klass {#lookup}

Du kan söka efter en viss klass genom att ta med klassens ID i sökvägen för en GET-begäran.

**API-format**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CONTAINER_ID}` | Den behållare som innehåller den klass som du vill hämta: `global` för en klass som skapats av Adobe eller `tenant` för en klass som ägs av organisationen. |
| `{CLASS_ID}` | The `meta:altId` eller URL-kodad `$id` av klassen som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran hämtar en klass med dess `meta:altId` värdet som anges i sökvägen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar informationen om klassen. Vilka fält som returneras beror på `Accept` huvud som skickades i begäran. Experimentera med olika `Accept` rubriker för att jämföra svaren och avgöra vilken rubrik som är bäst för dig.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{ORG_ID}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Skapa en klass {#create}

Du kan definiera en anpassad klass under `tenant` genom att göra en POST-förfrågan.

>[!IMPORTANT]
>
>När du komponerar ett schema baserat på en anpassad klass som du definierar, kan du inte använda standardfältgrupper. Varje fältgrupp definierar de klasser som de är kompatibla med i sina `meta:intendedToExtend` -attribut. När du börjar definiera fältgrupper som är kompatibla med den nya klassen (med `$id` i den nya klassen i `meta:intendedToExtend` fält i fältgruppen) kan du återanvända dessa fältgrupper varje gång du definierar ett schema som implementerar den klass du definierade. Se avsnitten om [skapa fältgrupper](./field-groups.md#create) och [skapa scheman](./schemas.md#create) om du vill ha mer information i deras respektive slutpunktsguider.
>
>Om du planerar att använda scheman som baseras på anpassade klasser i kundprofilen i realtid är det också viktigt att komma ihåg att fackscheman bara är konstruerade baserat på scheman som delar samma klass. Om du vill ta med ett schema av anpassad klass i unionen för en annan klass som [!UICONTROL XDM Individual Profile] eller [!UICONTROL XDM ExperienceEvent]måste du skapa en relation med ett annat schema som använder den klassen. Se självstudiekursen om [skapa en relation mellan två scheman i API:n](../tutorials/relationship-api.md) för mer information.

**API-format**

```http
POST /tenant/classes
```

**Begäran**

Begäran om att skapa (POST) en klass måste innehålla en `allOf` ett attribut som innehåller `$ref` till ett av två värden: `https://ns.adobe.com/xdm/data/record` eller `https://ns.adobe.com/xdm/data/time-series`. Dessa värden representerar det beteende som klassen baseras på (post- respektive tidsserierna). Mer information om skillnaderna mellan postdata och tidsseriedata finns i avsnittet om beteendetyper i [grunderna för schemakomposition](../schema/composition.md).

När du definierar en klass kan du även inkludera fältgrupper eller anpassade fält i klassdefinitionen. Detta gör att de tillagda fältgrupperna och fälten inkluderas i alla scheman som implementerar klassen. I följande exempelbegäran definieras klassen&quot;Property&quot; som innehåller information om olika egenskaper som ägs och drivs av ett företag. Den innehåller `propertyId` fält som ska inkluderas varje gång klassen används.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `_{TENANT_ID}` | The `TENANT_ID` namnutrymme för din organisation. Alla resurser som skapas av organisationen måste innehålla den här egenskapen för att undvika konflikter med andra resurser i [!DNL Schema Registry]. |
| `allOf` | En lista med resurser vars egenskaper ska ärvas av den nya klassen. En av `$ref` -objekt i arrayen definierar klassens beteende. I det här exemplet ärver klassen&quot;record&quot;-beteendet. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om den nyligen skapade klassen, inklusive `$id`, `meta:altId`och `version`. Dessa tre värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Utföra en GET-begäran till [lista alla klasser](#list) i `tenant` behållaren skulle nu inkludera klassen Property. Du kan också [utföra en uppslagsbegäran (GET)](#lookup) med URL-kodad `$id` om du vill visa den nya klassen direkt.

## Uppdatera en klass {#put}

Du kan ersätta en hel klass med en PUT-åtgärd, i princip skriva om resursen. När en klass uppdateras via en PUT-begäran måste texten innehålla alla fält som krävs när [skapa en ny klass](#create) i en POST.

>[!NOTE]
>
>Om du bara vill uppdatera en del av en klass i stället för att ersätta den helt, se avsnittet om [uppdatera en del av en klass](#patch).

**API-format**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | The `meta:altId` eller URL-kodad `$id` för klassen som du vill skriva om. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran skriver om en befintlig klass och ändrar dess `description` och `title` av ett av dess fält.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Svar**

Ett lyckat svar returnerar information om den uppdaterade klassen.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Uppdatera en del av en klass {#patch}

Du kan uppdatera en del av en klass med en PATCH-begäran. The [!DNL Schema Registry] stöder alla vanliga JSON-korrigeringsåtgärder, inklusive `add`, `remove`och `replace`. Mer information om JSON Patch finns i [Grundläggande API-guide](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Om du vill ersätta en hel resurs med nya värden i stället för att uppdatera enskilda fält, se avsnittet om [ersätta en klass med en PUT-åtgärd](#put).

**API-format**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | URL-kodad `$id` URI eller `meta:altId` för den klass som du vill uppdatera. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Exemplet nedan uppdaterar `description` av en befintlig klass och `title` av ett av dess fält.

Begärandetexten har formen av en array där varje listat-objekt representerar en specifik ändring i ett enskilt fält. Varje objekt innehåller den åtgärd som ska utföras (`op`), vilket fält åtgärden ska utföras på (`path`) och vilken information som ska ingå i åtgärden (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Svar**

Svaret visar att båda åtgärderna har utförts. The `description` har uppdaterats tillsammans med `title` i `propertyId` fält.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Ta bort en klass {#delete}

Ibland kan det vara nödvändigt att ta bort en klass från schemaregistret. Detta görs genom att utföra en DELETE-begäran med det klass-ID som anges i sökvägen.

**API-format**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{CLASS_ID}` | URL-kodad `$id` URI eller `meta:altId` för den klass som du vill ta bort. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka med en [sökbegäran (GET)](#lookup) för klassen. Du måste inkludera en `Accept` i begäran, men ska få HTTP-status 404 (Hittades inte) eftersom klassen har tagits bort från schemaregistret.
