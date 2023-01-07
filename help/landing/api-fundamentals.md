---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Grundläggande om Experience Platform API
description: I det här dokumentet finns en kort översikt över vissa underliggande tekniker och syntaxer som används för Experience Platform-API:er.
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Grundläggande om Experience Platform API

Adobe Experience Platform API:er använder flera underliggande tekniker och syntaxer som är viktiga att förstå för att effektivt hantera JSON-baserade [!DNL Platform] resurser. Dokumentet innehåller en kort översikt över dessa tekniker samt länkar till extern dokumentation för mer information.

## JSON-pekare {#json-pointer}

JSON-pekaren är en standardiserad strängsyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) för att identifiera specifika värden i JSON-dokument. En JSON-pekare är en sträng med tokens avgränsade med `/` -tecken, som anger antingen objektnycklar eller arrayindex, och token kan vara en sträng eller ett tal. JSON-pekarsträngar används i många PATCH-åtgärder för [!DNL Platform] API:er, som beskrivs senare i det här dokumentet. Mer information om JSON-pekaren finns i [Översiktsdokumentation för JSON-pekare](https://rapidjson.org/md_doc_pointer.html).

### Exempel på JSON-schemaobjekt

Följande JSON representerar ett förenklat XDM-schema vars fält kan refereras med JSON-pekarsträngar. Observera att alla fält som har lagts till med anpassade schemafältgrupper (till exempel `loyaltyLevel`) namnges under en `_{TENANT_ID}` objekt, medan fält som har lagts till med hjälp av huvudfältgrupper (t.ex. `fullName`) är inte det.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### Exempel på JSON-pekare baserat på schemaobjekt

| JSON-pekare | Löser till |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (Returnerar en referens till `fullName` -fält, från en huvudfältgrupp.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Returnerar en referens till `loyaltyLevel` -fält, från en anpassad fältgrupp.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>När du hanterar `xdm:sourceProperty` och `xdm:destinationProperty` attribut för [!DNL Experience Data Model] (XDM), alla `properties` nycklar måste vara **exkluderad** från JSON-pekarsträngen. Se [!DNL Schema Registry] Utvecklarhandbok för API på [beskrivare](../xdm/api/descriptors.md) för mer information.

## JSON Patch {#json-patch}

Det finns många PATCH-åtgärder för [!DNL Platform] API:er som accepterar JSON Patch-objekt för deras begärandatanyttolaster. JSON Patch är ett standardiserat format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) för att beskriva ändringar i ett JSON-dokument. Det gör att du kan definiera partiella uppdateringar av JSON utan att behöva skicka hela dokumentet i en begärandetext.

### Exempel på JSON-lagningsobjekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Typ av korrigeringsåtgärd. JSON Patch stöder flera olika åtgärdstyper, men inte alla PATCH-åtgärder i [!DNL Platform] API:er är kompatibla med alla åtgärdstyper. Tillgängliga åtgärdstyper är:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Den del av JSON-strukturen som ska uppdateras, identifieras med [JSON-pekare](#json-pointer) notation.

Beroende på vilken åtgärdstyp som anges i `op`kan JSON Patch-objektet kräva ytterligare egenskaper. Mer information om olika JSON Patch-åtgärder och deras syntax finns i [JSON Patch-dokumentation](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON-schema {#json-schema}

JSON-schema är ett format som används för att beskriva och validera JSON-datastrukturen. [Experience Data Model (XDM)](../xdm/home.md) utnyttjar JSON-schemafunktioner för att begränsa strukturen och formatet för inmatade kundupplevelsedata. Mer information om JSON Schema finns i [officiell dokumentation](https://json-schema.org/).

## Nästa steg

I det här dokumentet introducerades en del av de tekniker och syntaxer som används för att hantera JSON-baserade resurser för [!DNL Experience Platform]. Se [komma igång-guide](api-guide.md) för mer information om hur du arbetar med plattforms-API:er, inklusive bästa praxis. Svar på vanliga frågor finns i [Felsökningsguide för plattformen](troubleshooting.md).
