---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;mixin;Mixin;mixins;Mixins;create
solution: Experience Platform
title: Skapa en blandning
topic: developer guide
description: Blandningar är en uppsättning fält som används för att beskriva ett visst koncept, till exempel"adress" eller"profilinställningar". Det finns många standardblandningar att tillgå, eller så kan du definiera en egen när du vill hämta in information som är unik för din organisation.
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Skapa en blandning

Blandningar är en uppsättning fält som används för att beskriva ett visst koncept, till exempel&quot;adress&quot; eller&quot;profilinställningar&quot;. Det finns många standardblandningar att tillgå, eller så kan du definiera en egen när du vill hämta in information som är unik för din organisation. Varje blandning innehåller ett `meta:intendedToExtend` fält som listar de klasser som blandningen är kompatibel med.

Det kan vara praktiskt att granska alla tillgängliga mixar för att bekanta dig med fälten i varje. Du kan visa (GET) alla blandningar som är kompatibla med en viss klass genom att utföra en begäran mot var och en av behållarna &quot;global&quot; och &quot;tenant&quot;, och bara returnera de blandningar där fältet &quot;meta:intendedToExtend&quot; matchar klassen som du använder. Exemplen nedan returnerar alla blandningar som kan användas med [!DNL XDM Individual Profile] klassen:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

Exemplet på API-begäran nedan skapar en ny blandning i innehavarbehållaren.

**API-format**

```http
POST /tenant/mixins
```

**Begäran**

När du definierar en ny blandning måste den innehålla ett `meta:intendedToExtend` -attribut med en lista `$id` över de klasser som blandningen är kompatibel med. I det här exemplet är mixinen kompatibel med den egenskapsklass som du tidigare definierade. Anpassade fält måste kapslas under `_{TENANT_ID}` (som visas i exemplet) för att undvika kollisioner med andra blandningar eller fält från klassscheman. Observera att `propertyConstruction` fältet är en referens till datatypen som skapades i det föregående anropet.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om den nyligen skapade mixinen, inklusive `$id`, `meta:altId`och `version`. Dessa värden är skrivskyddade och tilldelas av [!DNL Schema Registry].

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
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
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
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Om du utför en GET-begäran om att lista alla blandningar i klientbehållaren skulle det nu inkludera blandningen Vehicle Details (fordonsinformation), eller så kan du utföra en sökning (GET)-begäran med den URL-kodade `$id` URI:n för att visa den nya mixinen direkt. Kom ihåg att inkludera `version` i huvudet Godkänn för alla uppslagsbegäranden.
