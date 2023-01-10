---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;fältgrupp;fältgrupp;fältgrupper;fältgrupper;datatyp;datatyp;datatyp;schemadesign;datatyp;datatyp;datatyp;datatyp;scheman;scheman;schemadesign;karta;karta;schema;
solution: Experience Platform
title: Begränsningar för XDM-fälttyp
description: En referens för fälttypsbegränsningar i Experience Data Model (XDM), inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API:t.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 2%

---

# Begränsningar för XDM-fälttyp

I XDM-scheman (Experience Data Model) begränsar fälttypen vilken typ av data som fältet kan innehålla. Det här dokumentet innehåller en översikt över varje huvudfälttyp, inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API för att tillämpa olika begränsningar.

## Komma igång

Innan du använder den här handboken bör du granska [grunderna för schemakomposition](./composition.md) för en introduktion till XDM-scheman, klasser och schemafältgrupper.

Om du planerar att definiera egna fälttyper i API:t rekommenderar vi att du börjar med [Utvecklarhandbok för schemaregister](../api/getting-started.md) om du vill lära dig hur du skapar fältgrupper och datatyper som du vill inkludera dina anpassade fält i. Om du använder användargränssnittet för Experience Platform för att skapa dina scheman kan du läsa guiden på [definiera fält i användargränssnittet](../ui/fields/overview.md) om du vill lära dig hur du implementerar begränsningar för fält som du definierar i anpassade fältgrupper och datatyper.

## Grundstruktur och exempel {#basic-types}

XDM byggs ovanpå JSON-schema och därför ärver XDM-fält en liknande syntax när de definierar sin typ. Att förstå hur olika fälttyper visas i JSON-schema kan hjälpa till att indikera basbegränsningarna för varje typ.

>[!NOTE]
>
>Se [Grundläggande API-guide](../../landing/api-fundamentals.md#json-schema) om du vill ha mer information om JSON-schema och andra underliggande tekniker i plattforms-API:er.

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
      <td>[!UICONTROL Double]</td>
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
{ "type": "integer", "maximum": 9007199254740991, "minimum": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "minimum": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "minimum": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "minimum": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alla datumformaterade strängar måste följa standarden ISO 8601 ([RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappa XDM-typer till andra format

Avsnitten nedan beskriver hur varje XDM-typ mappar till andra vanliga serialiseringsformat:

* [Parquet, Spark SQL och Java](#parquet)
* [Scala, .NET och CosmosDB](#scala)
* [MongoDB, Aerospike och Protobuf 2](#mongo)

>[!NOTE]
>
>Bland de standardtyper av XDM som anges i tabellerna nedan finns [!UICONTROL Map] typ ingår också. Kartor används i standardscheman när data representeras som nycklar som mappar till vissa värden, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.
>
>Många standardkomponenter för XDM använder karttyper, och du kan också [definiera anpassade kartfält](../tutorials/custom-fields-api.md#custom-maps) vid behov. Karttypen tas med i tabellerna nedan för att hjälpa dig att bestämma hur befintliga data ska mappas till XDM om de för närvarande lagras i något av formaten som listas nedan.

### Parquet, Spark SQL och Java {#parquet}

| XDM-typ | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Typ: `BYTE_ARRAY`<br>Anteckning: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Typ: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Typ: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Typ: `INT32`<br>Anteckning: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Typ: `INT32`<br>Anteckning: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Typ: `INT32`<br>Anteckning: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Typ: `INT32`<br>Anteckning: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Typ: `INT64`<br>Anteckning: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Typ: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annoterad grupp<br><br>(`<key-type>` måste vara `STRING`) | `MapType`<br><br>(`keyType` måste vara `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET och CosmosDB {#scala}

| XDM-typ | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (Ej tillämpligt) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike och Protobuf 2 {#mongo}

| XDM-typ | MongoDB | Aerospike | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix millisekunder) | `int64`<br>(Unix millisekunder) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix millisekunder) | `int64`<br>(Unix millisekunder) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binärt) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## Definiera XDM-fälttyper i API {#define-fields}

Med API:t för schemaregister kan du definiera anpassade fält med hjälp av format och valfria begränsningar. Se guiden [definiera anpassade fält i API:t för schemaregister](../tutorials/custom-fields-api.md) för mer information.
