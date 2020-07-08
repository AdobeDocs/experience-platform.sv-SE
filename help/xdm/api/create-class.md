---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en klass
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Skapa en klass

Den primära byggstenen för ett schema är en klass. Klassen innehåller den minsta uppsättning fält som måste definieras för att kunna hämta huvuddata från ett schema. Om du till exempel utformade ett schema för bilar och lastbilar skulle de troligen använda en klass som heter Vehicle som beskriver de grundläggande gemensamma egenskaperna för alla fordon.

Det finns flera standardklasser från Adobe och andra Experience Platform-partners, men du kan också definiera egna klasser och spara dem i schemaregistret. Du kan sedan skapa ett schema som implementerar den klass du skapade och definiera mixiner som är kompatibla med den nyligen definierade klassen.

>[!NOTE]
>
>När du komponerar ett schema baserat på en klass som du definierar, kan du inte använda standardblandningar. Varje mixin definierar de klasser som de är kompatibla med i deras `meta:intendedToExtend` -attribut. När du börjar definiera blandningar som är kompatibla med den nya klassen (genom att använda den nya klassen `$id` i fältet `meta:intendedToExtend` för blandningen), kan du återanvända dessa blandningar varje gång du definierar ett schema som implementerar den klass du definierade. Mer information finns i avsnitten om [att skapa mixins](create-mixin.md) och [skapa scheman](create-schema.md) .

**API-format**

```http
POST /tenant/classes
```

**Begäran**

Begäran om att skapa (POST) en klass måste innehålla ett `allOf` -attribut som innehåller ett `$ref` av två värden: `https://ns.adobe.com/xdm/data/record` eller `https://ns.adobe.com/xdm/data/time-series`. Dessa värden representerar det beteende som klassen baseras på (post- respektive tidsserierna). Mer information om skillnaderna mellan postdata och tidsseriedata finns i avsnittet om beteendetyper i [grunderna för schemakomposition](../schema/composition.md).

När du definierar en klass kan du även inkludera mixins eller anpassade fält i klassdefinitionen. Detta gör att de tillagda blandningarna och fälten inkluderas i alla scheman som implementerar klassen. I följande exempelbegäran definieras klassen&quot;Property&quot; som innehåller information om olika egenskaper som ägs och drivs av ett företag. Den innehåller ett `propertyId` fält som ska inkluderas varje gång klassen används.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `_{TENANT_ID}` | Namnutrymmet `TENANT_ID` för din organisation. Alla resurser som skapas av organisationen måste innehålla den här egenskapen för att undvika konflikter med andra resurser i schemaregistret. |
| `allOf` | En lista med resurser vars egenskaper ska ärvas av den nya klassen. Ett av `$ref` objekten i arrayen definierar klassens beteende. I det här exemplet ärver klassen&quot;record&quot;-beteendet. |

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och en nyttolast som innehåller information om den nyligen skapade klassen, inklusive `$id`, `meta:altId`och `version`. Dessa tre värden är skrivskyddade och tilldelas av schemaregistret.

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
    "imsOrg": "{IMS_ORG}",
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

En GET-begäran om att lista alla klasser i innehavarbehållaren skulle nu inkludera egenskapsklassen. Du kan också utföra en sökbegäran (GET) med den URL-kodade `$id` URI:n för att visa den nya klassen direkt. Se till att du tar med `version` i huvudet Godkänn när du utför en uppslagsbegäran.
