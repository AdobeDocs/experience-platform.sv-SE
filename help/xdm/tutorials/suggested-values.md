---
title: Hantera föreslagna värden i API
description: Lär dig hur du lägger till föreslagna värden i ett strängfält i API:t för schemaregister.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 19bd5d9c307ac6e1b852e25438ff42bf52a1231e
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Hantera föreslagna värden i API

För alla strängfält i Experience Data Model (XDM) kan du definiera en **enum** som begränsar de värden som fältet kan importera till en fördefinierad uppsättning. Om du försöker importera data till ett uppräkningsfält och värdet inte matchar någon av dem som definierats i konfigurationen, nekas intag.

I motsats till enum lägger du till **föreslagna värden** till ett strängfält begränsar inte de värden som kan importeras. Föreslagna värden påverkar i stället vilka fördefinierade värden som är tillgängliga i [Segmenteringsgränssnitt](../../segmentation/ui/overview.md) när strängfältet inkluderas som ett attribut.

>[!NOTE]
>
>Det finns en fördröjning på ungefär fem minuter för ett fälts uppdaterade föreslagna värden som ska återspeglas i segmenteringsgränssnittet.

Den här guiden beskriver hur du hanterar föreslagna värden med [API för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Anvisningar om hur du gör detta i användargränssnittet i Adobe Experience Platform finns i [Användargränssnittsguide för uppräkningar och föreslagna värden](../ui/fields/enum.md).

## Förutsättningar

I den här handboken förutsätts du känna till elementen i schemakompositionen i XDM och hur du använder API:t för schemaregister för att skapa och redigera XDM-resurser. Om du behöver en introduktion läser du i följande dokumentation:

* [Grunderna för schemakomposition](../schema/composition.md)
* [API-guide för schemaregister](../api/overview.md)

Vi rekommenderar att du läser [Utvecklingsregler för enum och föreslagna värden](../ui/fields/enum.md#evolution) om du uppdaterar befintliga fält. Om du hanterar föreslagna värden för scheman som ingår i en union kan du läsa [regler för att sammanfoga fasttext och föreslagna värden](../ui/fields/enum.md#merging).

## Disposition

I API:t är de begränsade värdena för **enum** fältet representeras av ett `enum` array, while a `meta:enum` -objektet innehåller egna visningsnamn för dessa värden:

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

För uppräkningsfält tillåts inte schemaregistret `meta:enum` att utsträckas utöver de värden som anges i `enum`, eftersom ett försök att importera strängvärden utanför dessa begränsningar inte godkänns i valideringen.

Du kan också definiera ett strängfält som inte innehåller ett `enum` -arrayen och använder bara `meta:enum` objekt att ange **föreslagna värden**:

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

Eftersom strängen inte har en `enum` matris för att definiera begränsningar, dess `meta:enum` kan utökas så att den innehåller nya värden.

## Hantera föreslagna värden för standardfält

För befintliga standardfält kan du [lägg till föreslagna värden](#add-suggested-standard) eller [ta bort föreslagna värden](#remove-suggested-standard).

### Lägg till föreslagna värden {#add-suggested-standard}

Utöka `meta:enum` av ett standardsträngfält kan du skapa [egen namnbeskrivning](../api/descriptors.md#friendly-name) för fältet i fråga i ett visst schema.

>[!NOTE]
>
>Föreslagna värden för strängfält kan bara läggas till på schemanivå. Med andra ord, utöka `meta:enum` för ett standardfält i ett schema påverkar inte andra scheman som använder samma standardfält.

Följande begäran lägger till föreslagna värden i standarden `eventType` fält (tillhandahålls av [Klassen XDM ExperienceEvent](../classes/experienceevent.md)) för det schema som identifieras under `sourceSchema`:

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
>Om standardfältet redan innehåller värden under `meta:enum`skriver inte de nya värdena från beskrivningen över de befintliga fälten och läggs till i stället:
>
>
```json
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

### Ta bort föreslagna värden {#remove-suggested-standard}

Om ett standardsträngfält har fördefinierade föreslagna värden kan du ta bort värden som du inte vill se i segmenteringen. Detta görs genom att skapa en [egen namnbeskrivning](../api/descriptors.md#friendly-name) för det schema som innehåller `xdm:excludeMetaEnum` -egenskap.

**API-format**

```http
POST /tenant/descriptors
```

**Begäran**

Följande begäran tar bort de föreslagna värdena &quot;[!DNL Web Form Filled Out]&quot; och &quot;[!DNL Media ping]&quot; for `eventType` i ett schema baserat på [Klassen XDM ExperienceEvent](../classes/experienceevent.md).

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

| Egenskap | Beskrivning |
| --- | --- |
| `@type` | Den typ av beskrivning som definieras. För en egen namnbeskrivning måste det här värdet anges till `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI för schemat där beskrivningen definieras. |
| `xdm:sourceVersion` | Huvudversionen av källschemat. |
| `xdm:sourceProperty` | Sökvägen till den specifika egenskap vars föreslagna värden du vill hantera. Sökvägen ska börja med ett snedstreck (`/`) och inte sluta med en. Inkludera inte `properties` i sökvägen (använd till exempel `/personalEmail/address` i stället för `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | Ett objekt som beskriver de föreslagna värden som ska exkluderas för fältet i segmentering. Nyckeln och värdet för varje post måste matcha de som ingår i originalet `meta:enum` av fältet för att bidraget ska kunna uteslutas. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och information om den nyskapade beskrivningen. De föreslagna värdena i `xdm:excludeMetaEnum` döljs nu i segmenteringsgränssnittet.

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
```

## Hantera föreslagna värden för ett anpassat fält {#suggested-custom}

Hantera `meta:enum` för ett anpassat fält kan du uppdatera fältets överordnade klass, fältgrupp eller datatyp genom en PATCH-begäran.

>[!WARNING]
>
>I motsats till standardfält uppdaterar du `meta:enum` för ett anpassat fält påverkar alla andra scheman som använder det fältet. Om du inte vill att ändringarna ska spridas över olika scheman kan du skapa en ny anpassad resurs i stället:
>
>* [Skapa en anpassad klass](../api/classes.md#create)
>* [Skapa en anpassad fältgrupp](../api/field-groups.md#create)
>* [Skapa en anpassad datatyp](../api/data-types.md#create)


Följande begäran uppdaterar `meta:enum` av ett fält för&quot;lojalitetsnivå&quot; som tillhandahålls av en anpassad datatyp:

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

I den här guiden beskrivs hur du hanterar föreslagna värden för strängfält i API:t för schemaregister. Se guiden [definiera anpassade fält i API](./custom-fields-api.md) om du vill ha mer information om hur du skapar olika fälttyper.
