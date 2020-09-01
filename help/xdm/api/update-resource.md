---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;update;Update;patch;PATCH
solution: Experience Platform
title: Uppdatera en resurs
description: 'Du kan ändra eller uppdatera resurser i innehavarbehållaren med hjälp av en PATCH-begäran. Schemaregistret stöder alla vanliga JSON-korrigeringsåtgärder, inklusive add, remove och replace. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Uppdatera en resurs

Du kan ändra eller uppdatera resurser i innehavarbehållaren med hjälp av en PATCH-begäran. Den [!DNL Schema Registry] stöder alla vanliga JSON-korrigeringsåtgärder, inklusive add, remove och replace.

Mer information om JSON Patch, inklusive tillgängliga åtgärder, finns i den officiella [JSON Patch-dokumentationen](http://jsonpatch.com/).

>[!NOTE]
>
>Om du vill ersätta en hel resurs med nya värden i stället för att uppdatera enskilda fält läser du dokumentet om hur du [ersätter en resurs med en PUT-åtgärd](replace-resource.md).

## Lägga till blandningar i ett schema

En av de vanligaste PATCH-åtgärderna är att lägga till tidigare definierade blandningar i ett XDM-schema, vilket visas i exemplet nedan.

**API-format**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska uppdateras från [!DNL Schema Library]. Giltiga typer är `datatypes`, `mixins`, `schemas`och `classes`. |
| `{RESOURCE_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` resursen. |

**Begäran**

Med en PATCH-åtgärd kan du uppdatera ett schema så att det innehåller fält som har definierats i en tidigare skapad blandning. För att kunna göra detta måste du utföra en PATCH-begäran till schemat med hjälp av dess `meta:altId` eller den URL-kodade `$id` URI:n.

Begärandetexten innehåller den åtgärd (`op`) som du vill utföra, var (`path`) du vill utföra åtgärden och vilken information (`value`) som du vill inkludera i åtgärden. I det här exemplet läggs blandningens `$id` värde till i både `meta:extends` - och `allOf` -fälten för målschemat.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
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

## Uppdatera enskilda fält för en resurs

Du kan också skicka PATCH-begäranden som gör flera ändringar i enskilda fält i en schemaregisterresurs.

**API-format**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beskrivning |
| --- | --- |
| `{RESOURCE_TYPE}` | Den typ av resurs som ska uppdateras från [!DNL Schema Library]. Giltiga typer är `datatypes`, `mixins`, `schemas`och `classes`. |
| `{RESOURCE_ID}` | Den URL-kodade `$id` URI:n eller `meta:altId` resursen. |

**Begäran**

Begärandetexten innehåller den åtgärd (`op`), plats (`path`) och information (`value`) som krävs för att uppdatera mixen. Den här begäran uppdaterar blandningen Egenskapsinformation för att ta bort fältet&quot;propertyCity&quot; och lägga till ett nytt&quot;propertyAddress&quot;-fält som refererar till en standarddatatyp som innehåller adressinformation. Det lägger också till ett nytt&quot;emailAddress&quot;-fält som refererar till en standarddatatyp med e-postinformation.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Svar**

Ett lyckat svar visar att åtgärderna har slutförts eftersom de nya fälten finns och fältet &quot;propertyCity&quot; har tagits bort.

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
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
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
