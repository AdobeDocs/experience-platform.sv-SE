---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Grundläggande om Adobe Experience Platform API
topic: getting started
description: I det här dokumentet finns en kort översikt över vissa underliggande tekniker och syntaxer som används för Experience Platform-API:er.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---


# Grundläggande om Adobe Experience Platform API

Adobe Experience Platform API:er använder flera underliggande tekniker och syntaxer som är viktiga att förstå för att effektivt hantera JSON-baserade [!DNL Platform]-resurser. Dokumentet innehåller en kort översikt över dessa tekniker samt länkar till extern dokumentation för mer information.

## JSON-pekare {#json-pointer}

JSON-pekaren är en standardiserad strängsyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) för att identifiera specifika värden i JSON-dokument. En JSON-pekare är en sträng med variabler som avgränsas med `/`-tecken, som anger antingen objektnycklar eller matrisindex, och variablerna kan vara en sträng eller ett tal. JSON-pekarsträngar används i många PATCH-åtgärder för [!DNL Platform] API:er, vilket beskrivs senare i det här dokumentet. Mer information om JSON-pekare finns i [översiktsdokumentationen för JSON-pekaren](https://rapidjson.org/md_doc_pointer.html).

### Exempel på JSON-schemaobjekt

Följande JSON representerar ett förenklat XDM-schema vars fält kan refereras med JSON-pekarsträngar. Observera att alla fält som har lagts till med anpassade blandningar (till exempel `loyaltyLevel`) namnges under ett `_{TENANT_ID}`-objekt, medan fält som har lagts till med kärnblandningar (till exempel `fullName`) inte namnges.

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
| `"/properties/person/properties/name/properties/fullName"` | (Returnerar en referens till fältet `fullName`, som tillhandahålls av en kärnblandning.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Returnerar en referens till fältet `loyaltyLevel`, som tillhandahålls av en anpassad blandning.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>När det gäller attributen `xdm:sourceProperty` och `xdm:destinationProperty` för [!DNL Experience Data Model] (XDM)-beskrivare måste alla `properties`-nycklar vara **exkluderade** från JSON-pekarsträngen. Mer information finns i [!DNL Schema Registry] API-utvecklarhandboken för [beskrivningar](../xdm/api/descriptors.md).

## JSON-lagning {#json-patch}

Det finns många PATCH-åtgärder för [!DNL Platform]-API:er som accepterar JSON-korrigeringsobjekt för sina begärannyttolaster. JSON Patch är ett standardiserat format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) för att beskriva ändringar i ett JSON-dokument. Det gör att du kan definiera partiella uppdateringar av JSON utan att behöva skicka hela dokumentet i en begärandetext.

### Exempel på JSON-lagningsobjekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Typ av korrigeringsåtgärd. JSON Patch har stöd för flera olika åtgärdstyper, men inte alla PATCH-åtgärder i [!DNL Platform] API:er är kompatibla med alla åtgärdstyper. Tillgängliga åtgärdstyper är:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Den del av JSON-strukturen som ska uppdateras, identifieras med  [JSON-](#json-pointer) sammanfogning.

Beroende på vilken åtgärdstyp som anges i `op` kan JSON Patch-objektet kräva ytterligare egenskaper. Mer information om de olika JSON Patch-åtgärderna och deras obligatoriska syntax finns i [JSON Patch documentation](http://jsonpatch.com/).

## JSON-schema

JSON-schema är ett format som används för att beskriva och validera JSON-datastrukturen. [Experience Data Model (XDM)](../xdm/home.md) utnyttjar JSON-schemafunktioner för att begränsa strukturen och formatet för inmatade kundupplevelsedata. Mer information om JSON-schema finns i [officiell dokumentation](https://json-schema.org/).

## Nästa steg

I det här dokumentet introducerades en del av de tekniker och syntaxer som används för att hantera JSON-baserade resurser för [!DNL Experience Platform]. Mer information om hur du arbetar med [!DNL Platform] API:er, inklusive bästa praxis och svar på vanliga frågor, finns i [Platsfelsökningsguiden](troubleshooting.md).