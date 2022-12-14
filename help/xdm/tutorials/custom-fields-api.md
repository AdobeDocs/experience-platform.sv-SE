---
title: Definiera XDM-fält i API:t för schemaregister
description: Lär dig hur du definierar olika fält när du skapar anpassade XDM-resurser (Experience Data Model) i API:t för schemaregister.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6277725cd69bc94325d3584177742df1a7fd4f95
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Definiera XDM-fält i API:t för schemaregister

Alla XDM-fält (Experience Data Model) definieras med hjälp av standarden [JSON-schema](https://json-schema.org/) begränsningar som gäller för deras fälttyp, med ytterligare begränsningar för fältnamn som används av Adobe Experience Platform. Med API:t för schemaregister kan du definiera anpassade fält i dina scheman genom att använda format och valfria begränsningar. XDM-fälttyperna visas av fältnivåattributet, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON-filen för fältet när du använder API:t (utom när [skapa anpassade mappningstyper](#custom-maps)). Bästa sättet är att använda JSON-schematyper (till exempel `string` och `integer`) med rätt min/max-begränsningar enligt tabellen nedan.

I den här handboken beskrivs lämplig formatering för att definiera olika fälttyper, inklusive de med valfria egenskaper. Mer information om valfria egenskaper och typspecifika nyckelord finns i [Dokumentation för JSON-schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Börja med att hitta den önskade fälttypen och använd exempelkoden som medföljer för att skapa din API-begäran för [skapa en fältgrupp](../api/field-groups.md#create) eller [skapa en datatyp](../api/data-types.md#create).

## [!UICONTROL String] {#string}

[!UICONTROL String] fält indikeras av `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

Du kan också begränsa vilka typer av värden som kan infogas för strängen genom följande ytterligare egenskaper:

* `pattern`: Ett regex-mönster som ska begränsas av.
* `minLength`: En minimilängd för strängen.
* `maxLength`: En maxlängd för strängen.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] fält indikeras av `type: string` med `format` egenskap inställd på `uri`. Inga andra egenskaper accepteras.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] fält måste använda `type: string`, med själva uppräkningsvärdena som anges under `enum` array:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

Du kan också ange kundadressetiketter för varje värde under en `meta:enum` egenskap, där varje etikett är nedtryckt till ett motsvarande värde under `enum`.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
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
  }
}
```

>[!NOTE]
>
>The `meta:enum` värdet gör **not** deklarera en uppräkning eller kör en datavalidering på egen hand. I de flesta fall anges strängar i `meta:enum` tillhandahålls också enligt `enum` för att säkerställa att data begränsas. Det finns dock vissa användningsområden där `meta:enum` tillhandahålls utan motsvarande `enum` array. Se självstudiekursen om [definiera föreslagna värden](../tutorials/suggested-values.md) för mer information.

Du kan också ange en `default` egenskap som anger standardvärdet `enum` värdet som fältet ska använda om inget värde anges.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
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

>[!IMPORTANT]
>
>Om nej `default` värdet anges och uppräkningsfältet anges till `required`kommer alla poster som saknar ett godkänt värde för det här fältet att misslyckas vid inmatning.

## [!UICONTROL Number] {#number}

Nummerfält indikeras av `type: number` och har inga andra obligatoriska egenskaper.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` typer används för alla numeriska typer, antingen heltal eller flyttal, medan [`integer` typer](#integer) används specifikt för heltal. Se [Dokumentation för JSON-schema för numeriska typer](https://json-schema.org/understanding-json-schema/reference/numeric.html) för mer information om användningsexempel för varje typ.

## [!UICONTROL Integer] {#integer}

[!UICONTROL Integer] fält indikeras av `type: integer` och inte ha några andra obligatoriska fält.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>while `integer` typer avser heltal specifikt, [`number` typer](#number) används för alla numeriska typer, antingen heltal eller flyttal. Se [Dokumentation för JSON-schema för numeriska typer](https://json-schema.org/understanding-json-schema/reference/numeric.html) för mer information om användningsexempel för varje typ.

Du kan begränsa heltalsomfånget genom att lägga till `minimum` och `maximum` egenskaper till definitionen. Flera andra numeriska typer som stöds av gränssnittet i Schema Builder är bara `integer` typer med specifika `minimum` och `maximum` begränsningar, som [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short)och [[!UICONTROL Byte]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Long] {#long}

Motsvarar en [!UICONTROL Long] fältet som skapas via gränssnittet i Schema Builder är ett [`integer` typfält](#integer) med specifik `minimum` och `maximum` värden (`-9007199254740992` och `9007199254740992`).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Short] {#short}

Motsvarar en [!UICONTROL Short] fältet som skapas via gränssnittet i Schema Builder är ett [`integer` typfält](#integer) med specifik `minimum` och `maximum` värden (`-32768` och `32768`).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

Motsvarar en [!UICONTROL Byte] fältet som skapas via gränssnittet i Schema Builder är ett [`integer` typfält](#integer) med specifik `minimum` och `maximum` värden (`-128` och `128`).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Boolean] {#boolean}

[!UICONTROL Boolean] fält indikeras av `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

Du kan också ange en `default` värdet som fältet ska använda när inget explicit värde anges vid inmatning.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Om nej `default` värdet anges och det booleska fältet anges till `required`kommer alla poster som saknar ett godkänt värde för det här fältet att misslyckas vid inmatning.

## [!UICONTROL Date] {#date}

[!UICONTROL Date] fält indikeras av `type: string` och `format: date`. Du kan också ange en array med `examples` om du vill visa ett exempel på en datumsträng för användare som anger data manuellt.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] fält indikeras av `type: string` och `format: date-time`. Du kan också ange en array med `examples` om du vill använda i de fall där du vill visa ett exempel på en datetime-sträng för användare som anger data manuellt.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Array] {#array}

[!UICONTROL Array] fält indikeras av `type: array` och `items` objekt som definierar schemat för de objekt som arrayen accepterar.

Du kan definiera arrayobjekt med primitiva typer, till exempel en array med strängar:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

Du kan också definiera arrayobjekten baserat på en befintlig datatyp genom att referera till `$id` av datatypen via en `$ref` -egenskap. Följande är en array med [!UICONTROL Payment Item] objekt:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Object] {#object}

[!UICONTROL Object] fält indikeras av `type: object` och `properties` objekt som definierar underegenskaper för schemafältet.

Varje delfält som definieras under `properties` kan definieras med valfri primitiv `type` eller genom att referera till en befintlig datatyp via en `$ref` egenskap som pekar på `$id` av den berörda datatypen:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

Du kan också definiera hela objektet genom att referera till en datatyp, förutsatt att datatypen i fråga själv definieras som `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Map] {#map}

Ett kartfält är i stort sett ett [`object`-typfält](#object) med en obegränsad uppsättning tangenter. Precis som objekt har kartor en `type` värde för `object`, men deras `meta:xdmType` anges explicit till `map`.

En karta **får inte** definiera egenskaper. Den **måste** definiera en `additionalProperties` schema som beskriver vilken typ av värden som finns i kartan (varje karta kan bara innehålla en enda datatyp). The `type` värdet måste vara antingen `string` eller `integer`.

Ett mappningsfält med strängtypsvärden definieras så här:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Mer information om hur du skapar anpassade kartfält finns i avsnittet nedan.

### Skapa anpassade mappningstyper {#custom-maps}

Objekten kan kommenteras med en `meta:xdmType` ange till `map` för att klargöra att ett objekt ska hanteras som om nyckeluppsättningen var obegränsad. Data som är inkapslade i mappningsfält måste använda strängnycklar och endast sträng- eller heltalsvärden (som bestäms av `additionalProperties.type`).

XDM har följande begränsningar för användning av detta lagringstips:

* Karttyper MÅSTE vara av typen `object`.
* Karttyper FÅR INTE ha egenskaper definierade (de definierar med andra ord tomma objekt).
* Karttyper MÅSTE innehålla en `additionalProperties.type` fält som beskriver värdena som kan placeras på kartan, antingen `string` eller `integer`.

Se till att du bara använder karttypsfält när det är absolut nödvändigt, eftersom de har följande prestandanackdelar:

* Svarstid från [Adobe Experience Platform Query Service](../../query-service/home.md) bryts ned från tre sekunder till tio sekunder för 100 miljoner poster.
* Kartor måste ha färre än 16 tangenter, annars riskerar de att försämras ytterligare.

Användargränssnittet för plattformen har även begränsningar för hur nycklarna för mappningsfält kan extraheras. Objekttypsfält kan expanderas, men kartor visas i stället som ett enda fält.

## Nästa steg

I den här handboken beskrivs hur du definierar olika fälttyper i API:t. Mer information om hur XDM-fälttyper formateras finns i handboken [Begränsningar för XDM-fälttyp](../schema/field-constraints.md).
