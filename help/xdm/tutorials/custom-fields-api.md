---
title: Definiera XDM-fält i API:t för schemaregister
description: Lär dig hur du definierar olika fält när du skapar anpassade XDM-resurser (Experience Data Model) i API:t för schemaregister.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Definiera XDM-fält i API:t för schemaregister

Alla XDM-fält (Experience Data Model) definieras med hjälp av standarden [JSON-schema](https://json-schema.org/) begränsningar som gäller för deras fälttyp, med ytterligare begränsningar för fältnamn som används av Adobe Experience Platform. Med API:t för schemaregister kan du definiera anpassade fält i dina scheman genom att använda format och valfria begränsningar. XDM-fälttyperna visas av fältnivåattributet, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` är ett systemgenererat värde och du behöver därför inte lägga till den här egenskapen i JSON-filen för fältet när du använder API:t (utom när [skapa anpassade mappningstyper](#maps)). Bästa sättet är att använda JSON-schematyper (till exempel `string` och `integer`) med rätt min/max-begränsningar enligt tabellen nedan.

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
    <br>Observera att <code>meta:enum</code> värdet gör <strong>not</strong> deklarera en uppräkning eller kör en datavalidering på egen hand. I de flesta fall anges strängar i <code>meta:enum</code> tillhandahålls också enligt <code>enum</code> för att säkerställa att data begränsas. Det finns dock vissa användningsområden där <code>meta:enum</code> tillhandahålls utan motsvarande <code>enum</code> array. Se självstudiekursen om <a href="../tutorials/suggested-values.md">definiera föreslagna värden</a> för mer information.
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
    <td>Ett mappningsfält är i princip ett objekttypsfält med en obegränsad uppsättning tangenter. Precis som objekt har kartor en <code>type</code> värde för <code>object</code>, men deras <code>meta:xdmType</code> anges explicit till <code>map</code>.<br><br>En karta <strong>får inte</strong> definiera egenskaper. Den <strong>måste</strong> definiera en <code>additionalProperties</code> schema som beskriver vilken typ av värden som finns i kartan (varje karta kan bara innehålla en enda datatyp). The <code>type</code> värdet måste vara antingen <code>string</code> eller <code>integer</code>.<br/><br/>Ett kartfält med strängtypsvärden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" }</pre>
    Mer information om hur du skapar anpassade mappningstyper i XDM finns i avsnittet nedan.
    </td>
  </tr>
</table>

## Skapa anpassade mappningstyper {#maps}

Objekten kan kommenteras med en `meta:xdmType` ange till `map` för att klargöra att ett objekt ska hanteras som om nyckeluppsättningen var obegränsad. Data som är inkapslade i mappningsfält måste använda strängnycklar och endast sträng- eller heltalsvärden (som bestäms av `additionalProperties.type`).

XDM har följande begränsningar för användning av detta lagringstips:

* Karttyper MÅSTE vara av typen `object`.
* Karttyper FÅR INTE ha egenskaper definierade (de definierar med andra ord tomma objekt).
* Karttyper MÅSTE innehålla en `additionalProperties.type` fält som beskriver värdena som kan placeras på kartan, antingen `string` eller `integer`.

Se till att du bara använder karttypsfält när det är absolut nödvändigt, eftersom de har följande prestandanackdelar:

* Svarstiden från Adobe Experience Platform Query Service försämras från tre sekunder till tio sekunder för 100 miljoner poster.
* Kartor måste ha färre än 16 tangenter, annars riskerar de att försämras ytterligare.

Användargränssnittet för plattformen har även begränsningar för hur nycklarna för mappningsfält kan extraheras. Objekttypsfält kan expanderas, men kartor visas i stället som ett enda fält.

## Nästa steg

I den här handboken beskrivs hur du definierar olika fälttyper i API:t. Mer information om hur XDM-fälttyper formateras finns i handboken [Begränsningar för XDM-fälttyp](../schema/field-constraints.md).
