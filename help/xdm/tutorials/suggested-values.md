---
title: Hantera föreslagna värden i API
description: Lär dig hur du lägger till föreslagna värden i ett strängfält i API:t för schemaregister.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Hantera föreslagna värden i API

För alla strängfält i Experience Data Model (XDM) kan du definiera en **enum** som begränsar de värden som fältet kan importera till en fördefinierad uppsättning. Om du försöker importera data till ett uppräkningsfält och värdet inte matchar någon av dem som definierats i konfigurationen, nekas intag.

Om du till skillnad från enum lägger till **föreslagna värden** i ett strängfält begränsas inte de värden som det kan importera. Föreslagna värden påverkar i stället vilka fördefinierade värden som är tillgängliga i [segmenteringsgränssnittet](../../segmentation/ui/overview.md) när strängfältet inkluderas som ett attribut.

>[!NOTE]
>
>Det finns en fördröjning på ungefär fem minuter för ett fälts uppdaterade föreslagna värden som ska återspeglas i segmenteringsgränssnittet.

Den här guiden beskriver hur du hanterar föreslagna värden med [API:t för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Anvisningar om hur du gör detta i Adobe Experience Platform användargränssnitt finns i [användargränssnittshandboken på enum och föreslagna värden](../ui/fields/enum.md).

## Förhandskrav

I den här handboken förutsätts du känna till elementen i schemakompositionen i XDM och hur du använder API:t för schemaregister för att skapa och redigera XDM-resurser. Om du behöver en introduktion läser du i följande dokumentation:

* [Grunderna för schemakomposition](../schema/composition.md)
* [API-guide för schemaregister](../api/overview.md)

Vi rekommenderar även att du granskar [everingsreglerna för enum och föreslagna värden](../ui/fields/enum.md#evolution) om du uppdaterar befintliga fält. Om du hanterar föreslagna värden för scheman som deltar i en union läser du [reglerna för att sammanfoga enum och föreslagna värden](../ui/fields/enum.md#merging).

## Disposition

I API representeras de begränsade värdena för ett **enum**-fält av en `enum`-array, medan ett `meta:enum`-objekt tillhandahåller egna visningsnamn för dessa värden:

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

För uppräkningsfält tillåter schemaregistret inte att `meta:enum` utökas utöver de värden som anges i `enum`, eftersom ett försök att importera strängvärden utanför dessa begränsningar inte klarar valideringen.

Du kan också definiera ett strängfält som inte innehåller en `enum`-array och bara använder `meta:enum`-objektet för att ange **föreslagna värden**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

Eftersom strängen inte har någon `enum`-matris för att definiera begränsningar, kan egenskapen `meta:enum` utökas så att den innehåller nya värden.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## Lägga till föreslagna värden i ett standardfält {#add-suggested-standard}

Om du vill utöka `meta:enum` för ett standardsträngfält kan du skapa en [egen namnbeskrivning](../api/descriptors.md#friendly-name) för fältet i fråga i ett visst schema.

>[!NOTE]
>
>Föreslagna värden för strängfält kan bara läggas till på schemanivå. Att utöka `meta:enum` för ett standardfält i ett schema påverkar alltså inte andra scheman som använder samma standardfält.

Följande begäran lägger till föreslagna värden i standardfältet `eventType` (tillhandahålls av klassen [ XDM ExperienceEvent](../classes/experienceevent.md)) för det schema som identifieras under `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

När du har använt beskrivningen svarar schemaregistret med följande när schemat hämtas (svaret trunkeras för utrymme):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>Om standardfältet redan innehåller värden under `meta:enum` skrivs inte de nya värdena från beskrivningen över de befintliga fälten och läggs till i stället:
>
>```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## Hantera föreslagna värden för ett anpassat fält {#suggested-custom}

Om du vill hantera `meta:enum` för ett anpassat fält kan du uppdatera fältets överordnade klass, fältgrupp eller datatyp via en PATCH-begäran.

>[!WARNING]
>
>Om du uppdaterar `meta:enum` för ett anpassat fält påverkas alla andra scheman som använder det fältet, till skillnad från standardfält. Om du inte vill att ändringarna ska spridas över olika scheman kan du skapa en ny anpassad resurs i stället:
>
>* [Skapa en anpassad klass](../api/classes.md#create)
>* [Skapa en anpassad fältgrupp](../api/field-groups.md#create)
>* [Skapa en anpassad datatyp](../api/data-types.md#create)

Följande begäran uppdaterar `meta:enum` för ett&quot;lojalitetsnivåfält&quot; som tillhandahålls av en anpassad datatyp:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

När ändringen har tillämpats svarar schemaregistret med följande när schemat hämtas (svaret trunkeras för utrymme):

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## Nästa steg

I den här guiden beskrivs hur du hanterar föreslagna värden för strängfält i API:t för schemaregister. Mer information om hur du skapar olika fälttyper finns i guiden [definierar anpassade fält i API](./custom-fields-api.md).
