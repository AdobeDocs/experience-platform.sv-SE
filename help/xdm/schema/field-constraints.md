---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;mixin;mixin;mixins;mixins;data type;data type;data types;data type;schema design;datatyp;datatyp;datatyp;datatyp;scheman;scheman;schema design;map;map;
solution: Experience Platform
title: Begränsningar för XDM-fälttyp
topic: overview
description: En referens för fälttypsbegränsningar i Experience Data Model (XDM), inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API:t.
translation-type: tm+mt
source-git-commit: c9ea7471bb18c92443a5e45c14c8505ef3ccf30d
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 1%

---


# Begränsningar för XDM-fälttyp

I XDM-scheman (Experience Data Model) begränsar fälttypen vilken typ av data som fältet kan innehålla. Det här dokumentet innehåller en översikt över varje huvudfälttyp, inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API för att tillämpa olika begränsningar.

## Komma igång

Innan du använder den här guiden bör du läsa igenom [grunderna för schemakomposition](./composition.md) för att få en introduktion till XDM-scheman, klasser och mixiner.

Om du planerar att definiera egna fälttyper i API:t rekommenderar vi att du börjar med [Utvecklarhandbok för schemaregister](../api/getting-started.md) för att lära dig hur du skapar blandningar och datatyper som du vill inkludera anpassade fält i. Om du använder användargränssnittet för Experience Platform för att skapa dina scheman kan du läsa guiden [definiera fält i användargränssnittet](../ui/fields/overview.md) för att lära dig hur du implementerar begränsningar för fält som du definierar i anpassade blandningar och datatyper.

## Grundstruktur och exempel

XDM byggs ovanpå JSON-schema och därför ärver XDM-fält en liknande syntax när de definierar sin typ. Att förstå hur olika fälttyper visas i JSON-schema kan hjälpa till att indikera basbegränsningarna för varje typ.

>[!NOTE]
>
>Mer information om JSON Schema och andra underliggande tekniker i API:er för plattformar finns i [Grundläggande guide för API](../../landing/api-fundamentals.md#json-schema).

I följande tabell visas hur varje XDM-typ representeras i JSON-schema, tillsammans med ett exempelvärde som överensstämmer med typen:

<table>
  <thead>
    <tr>
      <th>XDM-typ</th>
      <th>JSON-schema</th>
      <th>Exempel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL-sträng]</td>
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
{
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL-heltal]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL-byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 128,
  "minimum": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "format": "date-time"
}</pre>
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

**Alla datumformaterade strängar måste följa ISO 8601-standarden ([RFC 3339, avsnitt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## Mappa XDM-typer till andra format

Avsnitten nedan beskriver hur varje XDM-typ mappar till andra vanliga serialiseringsformat:

* [Parquet, Spark SQL och Java](#parquet)
* [Scala, .NET och CosmosDB](#scala)
* [MongoDB, Aerospike och Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Bland de XDM-standardtyper som anges i tabellerna nedan finns även typen [!UICONTROL Map]. Kartor används i standardscheman när data representeras som nycklar som mappar till vissa värden, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.
>
>Karttypsfält är reserverade för användning av branschschema och leverantörsschema och kan därför inte användas i anpassade resurser som du definierar. Karttypen tas med i tabellerna nedan och är endast avsedd att hjälpa dig att bestämma hur befintliga data ska mappas till XDM om de för närvarande lagras i något av formaten som listas nedan.

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
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` must be  `STRING`) | `MapType`<br><br>(`keyType` måste vara  `StringType`) | `java.util.Map` |

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

## Definiera XDM-fälttyper i API {#define-fields}

Alla XDM-fält definieras med standardbegränsningarna [JSON Schema](https://json-schema.org/) som gäller för deras fälttyp, med ytterligare begränsningar för fältnamn som framtvingas av [!DNL Experience Platform]. Med API:t för schemaregister kan du definiera ytterligare fälttyper genom att använda format och valfria begränsningar. XDM-fälttyper visas av fältnivåattributet `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON för fältet när du använder API:t. Det bästa sättet är att använda JSON-schematyper (till exempel `string` och `integer`) med rätt min/max-begränsningar enligt tabellen nedan.

Följande tabell visar lämplig formatering för att definiera olika fälttyper, inklusive de med valfria egenskaper. Mer information om valfria egenskaper och typspecifika nyckelord finns i [JSON Schema-dokumentationen](https://json-schema.org/understanding-json-schema/reference/type.html).

Börja med att hitta önskad fälttyp och använd exempelkoden som finns för att skapa din API-begäran för [skapa en mixin](../api/mixins.md#create) eller [skapa en datatyp](../api/data-types.md#create).

<table>
  <tr>
    <th>XDM-typ</th>
    <th>Valfria egenskaper</th>
    <th>Exempel</th>
  </tr>
  <tr>
    <td>[!UICONTROL-sträng]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
    "type": "string",
    "pattern": "^[A-Z]{2}$",
    "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Begränsade uppräkningsvärden anges under <code>enum</code>-arrayen, medan valfria kundvända etiketter för varje värde kan anges under <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Värde 1",
      "value2": "Värde 2",
      "value3": "Värde 3"
  },
  "default": "value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-heltal]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -2147483648,
  "maximum": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -128,
  "maximum": 128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "boolesk",
  "default": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-datum]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-matris]</td>
    <td></td>
    <td>En array med grundläggande skalära typer (t.ex. strängar):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "type": "string"
  }
}</pre>
      En array med objekt som definieras av ett annat schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-objekt]</td>
    <td></td>
    <td>Attributet <code>type</code> för varje underfält som definieras under <code>properties</code> kan definieras med valfri skalär typ:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "properties": {
    "fält1": {
      "type": "string"
    },
    "fält2": {
      "type": "number"
    }
  }
}</pre>
      Objekttypsfält kan definieras genom att referera till <code>$id</code> för en datatyp:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>En karta <strong>får inte</strong> definiera några egenskaper. Det <strong>måste</strong> definiera ett enda <code>additionalProperties</code>-schema för att beskriva värdetypen som finns i kartan (varje karta kan bara innehålla en enda datatyp). Värdena kan vara valfritt giltigt XDM <code>type</code>-attribut, eller en referens till ett annat schema med ett <code>$ref</code>-attribut.<br/><br/>Ett kartfält med strängtypsvärden:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "string"
  }
}</pre>
    Ett kartfält med strängarrayer för värden:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "array",
    "items": {
      "type": "string"
    }
  }
}</pre>
    Ett kartfält som refererar till en annan datatyp:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
