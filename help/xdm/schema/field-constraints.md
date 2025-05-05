---
keywords: Experience Platform;hem;populära ämnen;schema;schema;fältgrupp;fältgrupp;fältgrupper;fältgrupper;datatyp;datatyp;datatyp;schemadesign;datatyp;datatyp;datatyp;datatyp;scheman;scheman;schemadesign;karta;karta;
solution: Experience Platform
title: Begränsningar för XDM-fälttyp
description: En referens för fälttypsbegränsningar i Experience Data Model (XDM), inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API:t.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Begränsningar för XDM-fälttyp

I XDM-scheman (Experience Data Model) begränsar fälttypen vilken typ av data som fältet kan innehålla. Det här dokumentet innehåller en översikt över varje huvudfälttyp, inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API för att tillämpa olika begränsningar.

## Komma igång

Granska [grunderna för schemakomposition](./composition.md) innan du använder den här guiden för att få en introduktion till XDM-scheman, klasser och schemafältgrupper.

Om du planerar att definiera dina egna fälttyper i API rekommenderar vi att du börjar med [utvecklarhandboken för schemaregister](../api/getting-started.md) för att lära dig hur du skapar fältgrupper och datatyper som du vill inkludera dina anpassade fält i. Om du använder Experience Platform-gränssnittet för att skapa dina scheman kan du läsa guiden [definiera fält i användargränssnittet](../ui/fields/overview.md) för att lära dig hur du implementerar begränsningar för fält som du definierar i anpassade fältgrupper och datatyper.

## Grundstruktur och exempel {#basic-types}

XDM byggs ovanpå JSON-schema och därför ärver XDM-fält en liknande syntax när de definierar sin typ. Att förstå hur olika fälttyper visas i JSON-schema kan hjälpa till att indikera basbegränsningarna för varje typ. Anpassade fältnamn är inte skiftlägeskänsliga och måste ha olika namn på samma nivå i schemat.

>[!NOTE]
>
>Mer information om JSON-schema och andra underliggande tekniker i Experience Platform API:er finns i [API-handboken ](../../landing/api-fundamentals.md#json-schema).

I följande tabell visas hur varje XDM-typ representeras i JSON-schema, tillsammans med ett exempelvärde som överensstämmer med typen:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM-typ</th>
      <th>JSON-schema</th>
      <th>Exempel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
&rbrace;</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
&rbrace;</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
&rbrace;</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 128,
  "minimum": -128
&rbrace;</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date-time"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "boolesk"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alla datumformaterade strängar måste uppfylla standarden ISO 8601 ([RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappa XDM-typer till andra format

Avsnitten nedan beskriver hur varje XDM-typ mappar till andra vanliga serialiseringsformat:

* [Parquet, Spark SQL och Java](#parquet)
* [Scala, .NET och CosmosDB](#scala)
* [MongoDB, Aerospike och Protobuf 2](#mongo)

>[!NOTE]
>
>Bland de XDM-standardtyper som anges i tabellerna nedan ingår även typen [!UICONTROL Map]. Kartor används i standardscheman när data representeras som nycklar som mappar till vissa värden, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.
>
>Många standard-XDM-komponenter använder mappningstyper, och du kan även [definiera anpassade mappningsfält](../tutorials/custom-fields-api.md#custom-maps) om du vill. Karttypen tas med i tabellerna nedan för att hjälpa dig att bestämma hur befintliga data ska mappas till XDM om de för närvarande lagras i något av formaten som listas nedan.

### Parquet, Spark SQL och Java {#parquet}

| XDM-typ | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Typ: `BYTE_ARRAY`<br>Anteckning: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Number] | Typ: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Typ: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Typ: `INT32`<br>Anteckning: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Typ: `INT32`<br>Anteckning: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Typ: `INT32`<br>Anteckning: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Typ: `INT32`<br>Anteckning: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Typ: `INT64`<br>Anteckning: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Typ: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-kommenterad grupp <br><br>(`<key-type>` måste vara `STRING`) | `MapType`<br><br>(`keyType` måste vara `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET och CosmosDB {#scala}

| XDM-typ | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Number] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (Ej tillämpligt) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike och Protobuf 2 {#mongo}

| XDM-typ | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Number] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix millisekunder) | `int64`<br>(Unix millisekunder) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix millisekunder) | `int64`<br>(Unix millisekunder) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binärt) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## Definiera XDM-fälttyper i API {#define-fields}

Med API:t för schemaregister kan du definiera anpassade fält med hjälp av format och valfria begränsningar. Mer information finns i guiden [Definiera anpassade fält i API:t för schemaregister](../tutorials/custom-fields-api.md).
