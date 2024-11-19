---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Grundläggande om Experience Platform API
description: I det här dokumentet finns en kort översikt över vissa underliggande tekniker och syntaxer som används för Experience Platform-API:er.
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Grundläggande om Experience Platform API

Adobe Experience Platform API:er använder flera underliggande tekniker och syntaxer som är viktiga att förstå för att effektivt hantera JSON-baserade [!DNL Platform]-resurser. Dokumentet innehåller en kort översikt över dessa tekniker samt länkar till extern dokumentation för mer information.

## JSON-pekare {#json-pointer}

JSON-pekaren är en standardiserad strängsyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) för att identifiera specifika värden i JSON-dokument. En JSON-pekare är en sträng med variabler som avgränsas med `/` tecken, som anger antingen objektnycklar eller matrisindex, och tokenerna kan vara en sträng eller ett tal. JSON-pekarsträngar används i många PATCH-åtgärder för [!DNL Platform] API:er, vilket beskrivs senare i det här dokumentet. Mer information om JSON-pekare finns i [översiktsdokumentationen för JSON-pekaren](https://rapidjson.org/md_doc_pointer.html).

### Exempel på JSON-schemaobjekt

Följande JSON representerar ett förenklat XDM-schema vars fält kan refereras med JSON-pekarsträngar. Observera att alla fält som har lagts till med anpassade schemafältgrupper (till exempel `loyaltyLevel`) namnges under ett `_{TENANT_ID}` -objekt, medan fält som har lagts till med huvudfältgrupper (till exempel `fullName`) inte namnges.

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
| `"/properties/person/properties/name/properties/fullName"` | (Returnerar en referens till fältet `fullName`, som tillhandahålls av en huvudfältgrupp.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (Returnerar en referens till fältet `loyaltyLevel`, som tillhandahålls av en anpassad fältgrupp.) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>När du hanterar attributen `xdm:sourceProperty` och `xdm:destinationProperty` för [!DNL Experience Data Model] (XDM)-beskrivare måste alla `properties`-nycklar vara **exkluderade** från JSON-pekarsträngen. Mer information finns i [!DNL Schema Registry] API-utvecklarhandboken om [beskrivningar](../xdm/api/descriptors.md).

## JSON Patch {#json-patch}

Det finns många PATCH-åtgärder för [!DNL Platform] API:er som accepterar JSON Patch-objekt för deras begärandenyttolaster. JSON Patch är ett standardiserat format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) för att beskriva ändringar i ett JSON-dokument. Det gör att du kan definiera partiella uppdateringar av JSON utan att behöva skicka hela dokumentet i en begärandetext.

### Exempel på JSON-lagningsobjekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Korrigeringsåtgärd av typen. JSON Patch stöder flera olika åtgärdstyper, men inte alla PATCH-åtgärder i [!DNL Platform] API:er är kompatibla med alla åtgärdstyper. Tillgängliga åtgärdstyper är:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Den del av JSON-strukturen som ska uppdateras identifieras med [ JSON-pekarnotation](#json-pointer) .

Beroende på vilken åtgärdstyp som anges i `op` kan JSON Patch-objektet kräva ytterligare egenskaper. Mer information om olika JSON-korrigeringsåtgärder och deras syntax som krävs finns i [JSON-korrigeringsdokumentationen](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON-schema {#json-schema}

JSON-schema är ett format som används för att beskriva och validera JSON-datastrukturen. [Experience Data Model (XDM)](../xdm/home.md) använder JSON-schemafunktioner för att framtvinga begränsningar av strukturen och formatet för inkapslade kundupplevelsedata. Mer information om JSON-schema finns i den [officiella dokumentationen](https://json-schema.org/).

## Nästa steg

I det här dokumentet introducerades några av de tekniker och syntaxer som används för att hantera JSON-baserade resurser för [!DNL Experience Platform]. Mer information om hur du arbetar med plattforms-API:er finns i [komma igång-guiden](api-guide.md), inklusive bästa praxis. Svar på vanliga frågor finns i [felsökningsguiden för plattformen](troubleshooting.md).
