---
keywords: Experience Platform;hem;populära ämnen;schema;schema;schema;mixin;mixin;mixins;mixins;data type;data type;data types;data type;schema design;datatyp;datatyp;datatyp;datatyp;scheman;scheman;schema design;map;map;
solution: Experience Platform
title: Begränsningar för XDM-fälttyp
topic: overview
description: En referens för XDM-fälttypsbegränsningar, inklusive andra serialiseringsformat som de kan mappas till och hur du definierar egna fälttyper i API:t.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 3%

---


# Begränsningar för XDM-fälttyp

De XDM-fälttyper som du väljer för dina scheman begränsar vilka typer av data dessa fält kan innehålla. Det här dokumentet innehåller en översikt över varje huvudfälttyp, inklusive andra serialiseringsformat som de kan mappas till, och hur du definierar egna fälttyper i API för att tillämpa olika begränsningar.

## Komma igång

Innan du använder den här guiden bör du läsa igenom [grunderna för schemakomposition](./composition.md) för att få en introduktion till XDM-scheman, klasser och mixiner.

Om du planerar att definiera dina egna fälttyper rekommenderar vi att du börjar med [Utvecklarhandbok för schemaregister](../api/getting-started.md) för att lära dig hur du skapar blandningar och datatyper som du vill inkludera dina anpassade fält i.

## Mappa XDM-typer till andra format

Tabellen nedan beskriver mappningen mellan varje XDM-typ (`meta:xdmType`) och andra serialiseringsformat.

| XDM-typ<br>(meta:xdmType) | JSON<br>(JSON-schema) | Parquet<br>(typ/anteckning) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | text:sträng | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Sträng | System.String | Sträng | string | Sträng | string |
| tal | text:tal | DUBBELT | DoubleType | java.lang.Double | Dubbel | System.Double | Siffra | double | Dubbel | double |
| long | text:heltal<br>maximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Lång | System.Int64 | Siffra | long | Heltal | int64 |
| int | text:heltal<br>maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Siffra | int | Heltal | int32 |
| kort | text:heltal<br>maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Kort | System.Int16 | Siffra | int | Heltal | int32 |
| byte | type:integer<br>maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Siffra | int | Heltal | int32 |
| boolesk | text:boolesk | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | Heltal | Heltal | bool |
| datum | type:string<br>format:date<br>(RFC 3339, avsnitt 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Sträng | datum | Heltal<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:string<br>format:date-time<br>(RFC 3339, avsnitt 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Sträng | tidsstämpel | Heltal<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP kommenterade gruppen<br><br>&lt;<span>key_type</span>> MÅSTE vara STRING<br><br>&lt;<span>value_type</span>> typ av mappningsvärden | MapType<br><br>&quot;keyType&quot; MÅSTE vara StringType<br><br>&quot;valueType&quot; är en typ av mappningsvärden. | java.util.Map | Mappa | — | object | object | map | map&lt;<span>key_type, value_type</span>> |

## Definiera XDM-fälttyper i API {#define-fields}

XDM-scheman definieras med [JSON Schema](https://json-schema.org/)-standarder och grundläggande fälttyper, med ytterligare begränsningar för fältnamn som framtvingas av [!DNL Experience Platform]. Med [API:t för schemaregister](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) kan du definiera ytterligare fälttyper genom att använda format och valfria begränsningar. XDM-fälttyper visas av fältnivåattributet `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON-filen för fältet. Bästa sättet är att använda JSON-schematyper (till exempel sträng och heltal) med rätt min/max-begränsningar enligt tabellen nedan.

Följande tabell visar lämplig formatering för att definiera skalära fälttyper och mer specifika fälttyper med hjälp av valfria egenskaper. Mer information om valfria egenskaper och typspecifika nyckelord finns i [JSON Schema-dokumentationen](https://json-schema.org/understanding-json-schema/reference/type.html).

Börja med att hitta önskad fälttyp och använd exempelkoden som finns för att skapa din API-begäran för [skapa en mixin](../api/mixins.md#create) eller [skapa en datatyp](../api/data-types.md#create).

<table>
  <tr>
    <th>Önskad typ<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-schema)</th>
    <th>Exempel på kod</th>
  </tr>
  <tr>
    <td>string</td>
    <td>typ: sträng<br/><br/><strong>Valfria egenskaper:</strong><br/>
      <ul>
        <li>mönster</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>typ: sträng<br/>format: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: sträng)</td>
    <td>typ: string<br/><br/><strong>Valfri egenskap:</strong><br/>
      <ul>
        <li>standard</li>
      </ul>
    </td>
    <td>Ange kundtillvända alternativetiketter med "meta:enum":
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>tal</td>
    <td>typ: tal<br/>minimum: ±2,23×10^308<br/>max: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>typ: heltal<br/>maximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>typ: heltal<br/>maximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>kort</td>
    <td>typ: heltal<br/>maximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>typ: heltal<br/>maximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -128,
          "maximum": 128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>boolesk</td>
    <td><br/>typ: boolean<br/>{true, false}<br/><br/><strong>Valfri egenskap:</strong><br/>
      <ul>
        <li>standard</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "boolesk",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>datum</td>
    <td>typ: sträng<br/>format: datum</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date",
          "examples": ["2004-10-23"]
        }
      </pre>
      Datum enligt definition i <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, avsnitt 5.6</a>, där "fulldatum" = date-fullyear "-" date-month "-" date-mday (ÅÅÅÅ-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>typ: sträng<br/>format: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "format": "date-time",
          "examples": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Datum-Tid enligt definition i <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, avsnitt 5.6</a>, där "date-time" = "T" heltid:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>typ: array</td>
    <td>items.type kan definieras med vilken skalär som helst:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      </pre>
      Array med objekt som definieras av ett annat schema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "items": {
            "$ref": "id"
          }
        }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>typ: object</td>
    <td>egenskaper.{field}.type kan definieras med valfri skalär typ:
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
        }
      </pre>
      Fält av typen "object" som definieras av ett referensschema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>typ: object<br/><br/><strong>Obs!</strong><br/>Datatypen 'map' är reserverad för användning i bransch- och leverantörsschema och är inte tillgänglig för användning i innehavardefinierade fält. Den används i standardscheman när data representeras som nycklar som mappar till ett visst värde, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.</td>
    <td>En karta får INTE definiera några egenskaper. Det MÅSTE definiera ett enskilt"[!UICONTROL additionalProperties]"-schema för att beskriva värdetypen i 'map'. En karta i XDM kan bara innehålla en enda datatyp. Värdena kan vara vilken giltig XDM-schemadefinition som helst, inklusive en array eller ett objekt, eller som en referens till ett annat schema (via $ref).<br/><br/>Mappningsfält med värden av typen 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
          }
        }
      </pre>
    Mappa fält med värden som en array med strängar:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      </pre>
    Mappningsfält som refererar till ett annat schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "$ref": "id"
          }
        }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
</table>
