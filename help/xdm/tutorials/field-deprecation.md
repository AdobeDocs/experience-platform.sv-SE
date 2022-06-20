---
title: Föråldrade ett XDM-fält
description: Lär dig hur du ersätter XDM-fält (Experience Data Model) i API:t för schemaregister.
source-git-commit: dc400dce8a77f27347e767230faf7301afc7c1fb
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Föråldrade ett XDM-fält

I Experience Data Model (XDM) kan du ersätta ett fält i ett schema eller en anpassad resurs med hjälp av [API för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Det här dokumentet beskriver hur du ersätter fält för olika XDM-resurser.

## Komma igång

Den här självstudien kräver anrop till API:t för schemaregistret. Granska [utvecklarhandbok](../api/getting-started.md) för viktig information som du behöver känna till för att kunna göra dessa API-anrop. Detta inkluderar `{TENANT_ID}`, begreppet &quot;behållare&quot; och de rubriker som krävs för att göra en förfrågan (med särskild uppmärksamhet på `Accept` header och dess möjliga värden).

## Föråldrade ett anpassat fält {#custom}

Om du vill ersätta ett fält i en anpassad klass, fältgrupp eller datatyp uppdaterar du den anpassade resursen via en PUT- eller PATCH-begäran och lägger till attributet `meta:status: deprecated` till fältet i fråga.

>[!NOTE]
>
>Allmän information om hur du uppdaterar anpassade resurser i XDM finns i följande dokumentation:
>
>* [Uppdatera en klass](../api/classes.md#patch)
>* [Uppdatera en fältgrupp](../api/field-groups.md#patch)
>* [Uppdatera en datatyp](../api/data-types.md#patch)


Exemplet på API-anrop nedan tar bort ett fält i en anpassad datatyp.

**API-format**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Begäran**

Följande begäran tar bort `expansionArea` fält för en datatyp som beskriver en fastighet.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Svar**

Ett lyckat svar returnerar uppdateringsinformationen för den anpassade resursen, där det borttagna fältet innehåller ett `meta:status` värde för `deprecated`. Exemplet nedan har trunkerats för blanksteg.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
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
  "imsOrg": "{IMS_ORG}",
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

## Ta bort ett standardfält i ett schema {#standard}

Fält från standardklasser, fältgrupper och datatyper kan inte tas bort direkt. I stället kan du förskjuta användningen av dem i de enskilda scheman som använder dessa standardresurser genom att använda en beskrivning.

### Skapa en beskrivning för fältborttagning {#create-descriptor}

Om du vill skapa en beskrivning för de schemafält som du vill ta bort gör du en POST till `/tenant/descriptors` slutpunkt.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Beskrivningstypen. För en deskriptor för fältborttagning måste det här värdet anges till `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` för det schema som du använder beskrivningen på. |
| `xdm:sourceVersion` | Den version av schemat som du tillämpar beskrivningen på. Ska anges till `1`. |
| `xdm:sourceProperty` | Sökvägen till egenskapen i schemat som du tillämpar beskrivningen på. Om du vill tillämpa beskrivningen på flera egenskaper kan du ange en lista med sökvägar i form av en array (till exempel `["/firstName", "/lastName"]`). |

**Svar**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Verifiera det inaktuella fältet {#verify-deprecation}

När beskrivningen har tillämpats kan du verifiera om fältet har tagits bort genom att leta upp schemat i fråga och använda rätt `Accept` header.

>[!NOTE]
>
>Visar inaktuella fält när det inte finns stöd för att visa scheman.

**API-format**

```http
GET /tenant/schemas
```

**Begäran**

Om du vill ta med information om inaktuella fält i API-svaret måste du ange `Accept` sidhuvud till `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Svar**

Ett lyckat svar returnerar informationen om schemat, där det borttagna fältet innehåller ett `meta:status` värde för `deprecated`. Exemplet nedan har trunkerats för blanksteg.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Nästa steg

I det här dokumentet beskrivs hur XDM-fält skrivs ut med API:t för schemaregister. Mer information om hur du konfigurerar fält för anpassade resurser finns i handboken [definiera XDM-fält i API](./custom-fields-api.md). Mer information om hur du hanterar beskrivningar finns i [slutpunktshandbok för beskrivningar](../api/descriptors.md).
