---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;fältgrupp;fältgrupp;fältgrupper;fältgrupper;datatyp;datatyp;datatyp;schemadesign;datatyp;datatyp;datatyp;datatyp;scheman;scheman;schemadesign;karta;karta;schema;
solution: Experience Platform
title: Begränsningar för XDM-fälttyp
topic-legacy: overview
description: En referens för fälttypsbegränsningar i Experience Data Model (XDM), inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API:t.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 1%

---

# Begränsningar för XDM-fälttyp

I XDM-scheman (Experience Data Model) begränsar fälttypen vilken typ av data som fältet kan innehålla. Det här dokumentet innehåller en översikt över varje huvudfälttyp, inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API för att tillämpa olika begränsningar.

## Komma igång

Innan du använder den här handboken bör du granska [grunderna för schemakomposition](./composition.md) för en introduktion till XDM-scheman, klasser och schemafältgrupper.

Om du planerar att definiera egna fälttyper i API:t rekommenderar vi att du börjar med [Utvecklarhandbok för schemaregister](../api/getting-started.md) om du vill lära dig hur du skapar fältgrupper och datatyper som du vill inkludera dina anpassade fält i. Om du använder användargränssnittet för Experience Platform för att skapa dina scheman kan du läsa guiden på [definiera fält i användargränssnittet](../ui/fields/overview.md) om du vill lära dig hur du implementerar begränsningar för fält som du definierar i anpassade fältgrupper och datatyper.

## Grundstruktur och exempel

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

>[!IMPORTANT]
>
>Bland de standardtyper av XDM som anges i tabellerna nedan finns [!UICONTROL Map] typ ingår också. Kartor används i standardscheman när data representeras som nycklar som mappar till vissa värden, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.
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

Alla XDM-fält definieras med hjälp av standarden [JSON-schema](https://json-schema.org/) begränsningar som gäller för deras fälttyp, med ytterligare begränsningar för fältnamn som framtvingas av [!DNL Experience Platform]. Med API:t för schemaregister kan du definiera ytterligare fälttyper genom att använda format och valfria begränsningar. XDM-fälttyperna visas av fältnivåattributet, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON för fältet när du använder API:t. Bästa sättet är att använda JSON-schematyper (till exempel `string` och `integer`) med rätt min/max-begränsningar enligt tabellen nedan.

Följande tabell visar lämplig formatering för att definiera olika fälttyper, inklusive de med valfria egenskaper. Mer information om valfria egenskaper och typspecifika nyckelord finns i [Dokumentation för JSON-schema](https://json-schema.org/understanding-json-schema/reference/type.html).

Börja med att hitta den önskade fälttypen och använd exempelkoden som medföljer för att skapa din API-begäran för [skapa en fältgrupp](../api/field-groups.md#create) eller [skapa en datatyp](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>XDM-typ</th>
    <th>Valfria egenskaper</th>
    <th>Exempel</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
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
    <td>Begränsade uppräkningsvärden anges under <code>enum</code> matris, medan valfria kundvända etiketter för varje värde kan anges under <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Värde 1", "värde2": "Värde 2", "värde3": "Value 3" }, "default": "value1" }</pre>
    <br>Observera att <code>meta:enum</code> värdet gör <strong>not</strong> deklarera en uppräkning eller kör en datavalidering på egen hand. I de flesta fall anges strängar i <code>meta:enum</code> tillhandahålls också enligt <code>enum</code> för att säkerställa att data begränsas. Det finns dock vissa användningsområden där <code>meta:enum</code> tillhandahålls utan motsvarande <code>enum</code> array. Se självstudiekursen om <a href="../tutorials/extend-soft-enum.md">utöka valfria uppräkningar</a> för mer information.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -9007199254740992, "maximum": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -2147483648, "maximum": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -32768, "maximum": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -128, "maximum": 128 }</pre>
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
"sampleField": { "type": "boolean", "default": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "examples": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "examples": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>En array med grundläggande skalära typer (t.ex. strängar):
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "type": "string" }</pre>
      En array med objekt som definieras av ett annat schema:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>The <code>type</code> attribut för varje delfält som definieras under <code>properties</code> kan definieras med valfri skalär typ:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } }</pre>
      Objekttypsfält kan definieras genom att referera till <code>$id</code> av en datatyp:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>En karta <strong>får inte</strong> definiera egenskaper. Den <strong>måste</strong> definiera en <code>additionalProperties</code> schema som beskriver vilken typ av värden som finns i kartan (varje karta kan bara innehålla en enda datatyp). Värdena kan vara valfri giltig XDM <code>type</code> eller en referens till ett annat schema med ett <code>$ref</code> -attribut.<br/><br/>Ett kartfält med strängtypsvärden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "string" }</pre>
    Ett kartfält med strängarrayer för värden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } }</pre>
    Ett kartfält som refererar till en annan datatyp:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
</table>
