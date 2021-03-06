---
title: Lägg till föreslagna värden i ett fält
description: Lär dig hur du lägger till föreslagna värden i ett strängfält i API:t för schemaregister.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Lägga till föreslagna värden i ett fält

I Experience Data Model (XDM) representerar ett uppräkningsfält ett strängfält som är begränsat till en fördefinierad delmängd av värden. Uppräkningsfält kan ge validering för att säkerställa att importerade data överensstämmer med en uppsättning godkända värden. Du kan också definiera en uppsättning föreslagna värden för ett strängfält utan att tvinga dem som begränsningar.

I [API för schemaregister](https://developer.adobe.com/experience-platform-apis/references/schema-registry/), representeras de begränsade värdena för ett uppräkningsfält av ett `enum` array, while a `meta:enum` -objektet innehåller egna visningsnamn för dessa värden:

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

Du kan också definiera ett strängfält som inte innehåller ett `enum` -arrayen och använder bara `meta:enum` objekt för att ange föreslagna värden:

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

Eftersom strängen inte har en `enum` matris för att definiera begränsningar, dess `meta:enum` kan utökas så att den innehåller nya värden. I den här självstudien beskrivs hur du lägger till föreslagna värden i standardsträngfält och anpassade strängfält i API:t för schemaregister.

## Förutsättningar

I den här handboken förutsätts du känna till elementen i schemakompositionen i XDM och hur du använder API:t för schemaregister för att skapa och redigera XDM-resurser. Om du behöver en introduktion läser du i följande dokumentation:

* [Grunderna för schemakomposition](../schema/composition.md)
* [API-guide för schemaregister](../api/overview.md)

## Lägga till föreslagna värden i ett standardfält

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

## Lägga till föreslagna värden i ett anpassat fält

Utöka `meta:enum` för ett anpassat fält kan du uppdatera fältets överordnade klass, fältgrupp eller datatyp genom en PATCH-begäran.

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

I den här guiden beskrivs hur du lägger till föreslagna värden i strängfält i API:t för schemaregister. Se guiden [definiera anpassade fält i API](./custom-fields-api.md) om du vill ha mer information om hur du skapar olika fälttyper.
