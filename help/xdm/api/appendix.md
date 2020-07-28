---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schema Registry developer appendix
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 2%

---


# Bilaga

Det här dokumentet innehåller ytterligare information om hur du arbetar med [!DNL Schema Registry] API:t.

## Kompatibilitetsläge

[!DNL Experience Data Model] (XDM) är en öppet dokumenterad specifikation som drivs av Adobe för att förbättra interoperabiliteten, uttrycksfullheten och styrkan i digitala upplevelser. Adobe underhåller källkoden och de formella XDM-definitionerna i ett [öppen källkodsprojekt på GitHub](https://github.com/adobe/xdm/). Dessa definitioner är skrivna i XDM Standard Notation, med JSON-LD (JavaScript Object Notation for Linked Data) och JSON Schema som grammatik för att definiera XDM-scheman.

När du tittar på formella XDM-definitioner i den offentliga databasen ser du att standard-XDM skiljer sig från det du ser i Adobe Experience Platform. Det du ser i [!DNL Experience Platform] kallas Kompatibilitetsläge och ger en enkel mappning mellan standard-XDM och det sätt som det används i [!DNL Platform].

### Så här fungerar kompatibilitetsläget

Kompatibilitetsläge gör att XDM JSON-LD-modellen kan arbeta med befintlig datainfrastruktur genom att ändra värden inom standard-XDM samtidigt som semantiken förblir densamma. Den använder en kapslad JSON-struktur och visar scheman i ett trädliknande format.

Den största skillnaden mellan standard-XDM och kompatibilitetsläge är borttagningen av &quot;xdm:&quot;-prefixet för fältnamn.

Följande är en jämförelse sida vid sida som visar födelsedagsrelaterade fält (med&quot;description&quot;-attribut borttagna) i både standard-XDM och kompatibilitetsläge. Observera att fälten för kompatibilitetsläge innehåller en referens till XDM-fältet och dess datatyp i attributen &quot;meta:xdmField&quot; och &quot;meta:xdmType&quot;.

<table>
  <th>Standard XDM</th>
  <th>Kompatibilitetsläge</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Födelsedatum", "typ": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Födelsedatum", "typ": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Födelseår", "typ": "integer", "minimum": 1, "maximum": 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Födelsedatum", "typ": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Födelsedatum", "typ": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Födelseår", "typ": "integer", "minimum": 1, "maximum": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Varför krävs kompatibilitetsläge?

Adobe Experience Platform är utformat för att fungera med flera lösningar och tjänster, var och en med sina egna tekniska utmaningar och begränsningar (t.ex. hur vissa tekniker hanterar specialtecken). Kompatibilitetsläge har utvecklats för att övervinna dessa begränsningar.

De flesta [!DNL Experience Platform] tjänster, inklusive [!DNL Catalog], [!DNL Data Lake]och [!DNL Real-time Customer Profile] användning [!DNL Compatibility Mode] i stället för standard-XDM. API:t [!DNL Schema Registry] använder också [!DNL Compatibility Mode]och exemplen i det här dokumentet visas alla med [!DNL Compatibility Mode].

Det är värt att veta att en mappning görs mellan standard-XDM och hur den är opererad i [!DNL Experience Platform], men det bör inte påverka din användning av [!DNL Platform] tjänster.

Du har tillgång till projektet med öppen källkod, men när det gäller att interagera med resurser via [!DNL Schema Registry], ger API-exemplen i det här dokumentet de bästa metoder du bör känna till och följa.

## Definiera XDM-fälttyper i API {#field-types}

XDM-scheman definieras med JSON-schemastandarder och grundläggande fälttyper, med ytterligare begränsningar för fältnamn som används av [!DNL Experience Platform]. Med XDM kan du definiera ytterligare fälttyper genom att använda format och valfria begränsningar. XDM-fälttyperna visas med fältnivåattributet `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON-filen för fältet. Bästa sättet är att använda JSON-schematyper (till exempel sträng och heltal) med rätt min/max-begränsningar enligt tabellen nedan.

Följande tabell visar lämplig formatering för att definiera skalära fälttyper och mer specifika fälttyper med hjälp av valfria egenskaper. Mer information om valfria egenskaper och typspecifika nyckelord finns i dokumentationen för [JSON-schemat](https://json-schema.org/understanding-json-schema/reference/type.html).

Börja med att hitta önskad fälttyp och använd exempelkoden som medföljer för att skapa din API-begäran.

<table>
  <tr>
    <th>Önskad typ<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-schema)</th>
    <th>Exempel på kod</th>
  </tr>
  <tr>
    <td>string</td>
    <td>typ:<br/><br/><strong>stringOptional-egenskaper:</strong><br/>
      <ul>
        <li>mönster</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>typ:<br/>stringformat: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: sträng)</td>
    <td>typ: Egenskapen<br/><br/><strong>stringOptional:</strong><br/>
      <ul>
        <li>standard</li>
      </ul>
    </td>
    <td>Ange kundtillvända alternativetiketter med "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Värde 1", "värde2": "Värde 2", "värde3": "Value 3" }, "default": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>tal</td>
    <td>typ: minsta<br/>antal: ±2,23×10^308<br/>maximum: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>typ:<br/>integermaximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -9007199254740992, "maximum": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>typ:<br/>integermaximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -2147483648, "maximum": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>kort</td>
    <td>typ:<br/>integermaximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -32768, "maximum": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>typ:<br/>integermaximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -128, "maximum": 128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>boolesk</td>
    <td><br/>typ: boolesk<br/>{true, false}<br/><br/><strong>Valfri egenskap:</strong><br/>
      <ul>
        <li>standard</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "boolean", "default": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>datum</td>
    <td>typ:<br/>stringformat: datum</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date", "examples": ["2004-10-23"] }
      </pre>
      Datum enligt definition i <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, avsnitt 5.6</a>, där "fulldatum" = datum-fullår "-" datum-månad "-" datum-mdag (ÅÅÅÅ-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>typ:<br/>stringformat: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date-time", "examples": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Datum-Tid enligt definition i <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, avsnitt 5.6</a>, där "date-time" = "T" heltid:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>typ: array</td>
    <td>items.type kan definieras med vilken skalär som helst:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" }
      </pre>
      Array med objekt som definieras av ett annat schema:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>typ: object</td>
    <td>egenskaper.{field}.type kan definieras med valfri skalär typ:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } }
      </pre>
      Fält av typen "object" som definieras av ett referensschema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>typ:<br/><br/><strong>objectNote:</strong><br/>Användning av datatypen"map" är reserverad för användning av bransch- och leverantörsschema och är inte tillgänglig för användning i innehavardefinierade fält. Den används i standardscheman när data representeras som nycklar som mappar till ett visst värde, eller där nycklar inte rimligen kan inkluderas i ett statiskt schema och måste behandlas som datavärden.</td>
    <td>En karta får INTE definiera några egenskaper. Det MÅSTE definiera ett enskilt"[!UICONTROL additionalProperties]"-schema för att beskriva värdetypen i 'map'. En karta i XDM kan bara innehålla en enda datatyp. Värdena kan vara vilken giltig XDM-schemadefinition som helst, inklusive en array eller ett objekt, eller som en referens till ett annat schema (via $ref).<br/><br/>Mappningsfält med värden av typen 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "string" }
      </pre>
    Mappa fält med värden som en array med strängar:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } }
      </pre>
    Mappningsfält som refererar till ett annat schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "$ref": "id" }
      </pre>
      Där "id" är {id} för referensschemat.
    </td>
  </tr>
</table>


## Mappa XDM-typer till andra format

Tabellen nedan beskriver mappningen mellan&quot;meta:xdmType&quot; och andra serialiseringsformat.

| XDM-typ<br>(meta:xdmType) | JSON<br>(JSON-schema) | Parquet<br>(typ/anteckning) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | text:sträng | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Sträng | System.String | Sträng | string | Sträng | string |
| tal | text:tal | DUBBELT | DoubleType | java.lang.Double | Dubbel | System.Double | Siffra | double | Dubbel | double |
| long | text:<br>integermaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Lång | System.Int64 | Siffra | long | Heltal | int64 |
| int | text:<br>integermaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Siffra | int | Heltal | int32 |
| kort | text:<br>integermaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Kort | System.Int16 | Siffra | int | Heltal | int32 |
| byte | text:<br>heltalMaximal:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Siffra | int | Heltal | int32 |
| boolesk | text:boolesk | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | Heltal | Heltal | bool |
| datum | text:<br>stringformat:datum<br>(RFC 3339, avsnitt 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Sträng | datum | Heltal<br>(unix millis) | int64<br>(unix millis) |
| date-time | text:<br>stringformat:datum-tid<br>(RFC 3339, avsnitt 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Sträng | tidsstämpel | Heltal<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP-kommenterad grupp<br><br>&lt;<span>key_type</span>> MÅSTE vara STRING<br><br>&lt;<span>value_type</span>> typ av mappningsvärden | MapType<br><br>&quot;keyType&quot; MÅSTE vara StringType<br><br>&quot;valueType&quot; är en typ av mappningsvärden. | java.util.Map | Mappa | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
