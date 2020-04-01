---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Grundläggande om API:er för Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: c94f065a5d56ac495dd2d541531aaec94c187612

---


# Grundläggande om API:er för Adobe Experience Platform

Adobe Experience Platform API:er använder flera underliggande tekniker och syntaxer som är viktiga att förstå för att effektivt hantera JSON-baserade plattformsresurser. Dokumentet innehåller en kort översikt över dessa tekniker samt länkar till extern dokumentation för mer information.

## JSON-pekare {#json-pointer}

JSON-pekaren är en standardiserad strängsyntax ([RFC 6901](https://tools.ietf.org/html/rfc6901)) som används för att identifiera specifika värden i JSON-dokument. En JSON-pekare är en sträng med variabler som avgränsas med `/` tecken, som anger antingen objektnycklar eller matrisindex, och token kan vara en sträng eller ett tal. JSON-pekarsträngar används i många PATCH-åtgärder för plattforms-API:er, vilket beskrivs senare i det här dokumentet. Mer information om JSON-pekare finns i översiktsdokumentationen för [JSON-pekaren](https://rapidjson.org/md_doc_pointer.html).

### Exempel på JSON-schemaobjekt

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### Exempel på JSON-pekare baserat på schemaobjekt

| JSON-pekare | Löser till |
|--- | ---|
| `"/title"` | &quot;Information om lojalitetsmedlem&quot; |
| `"/definitions/loyalty"` | (Returnerar innehållet i `loyalty` objektet) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note]
>När du hanterar attributen `xdm:sourceProperty` och `xdm:destinationProperty` attributen för XDM-beskrivningar (Experience Data Model) måste alla `properties` nycklar **uteslutas** från JSON-pekarsträngen. Mer information finns i underhandboken för programmeringsregistrets API-utvecklare om [beskrivningar](../xdm/api/descriptors.md) .

## JSON Patch

Det finns många PATCH-åtgärder för plattforms-API:er som accepterar JSON Patch-objekt för deras begärandenyttolaster. JSON Patch är ett standardiserat format ([RFC 6902](https://tools.ietf.org/html/rfc6902)) för att beskriva ändringar i ett JSON-dokument. Det gör att du kan definiera partiella uppdateringar av JSON utan att behöva skicka hela dokumentet i en begärandetext.

### Exempel på JSON-lagningsobjekt

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`: Typ av korrigeringsåtgärd. JSON Patch stöder flera olika åtgärdstyper, men alla PATCH-åtgärder i Platform API:er är inte kompatibla med alla åtgärdstyper. Tillgängliga åtgärdstyper är:
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`: Den del av JSON-strukturen som ska uppdateras, identifieras med [JSON-pekarnotation](#json-pointer) .

Beroende på vilken åtgärdstyp som anges i `op`kan JSON Patch-objektet kräva ytterligare egenskaper. Mer information om de olika JSON Patch-åtgärderna och deras syntax som krävs finns i dokumentationen [för](http://jsonpatch.com/)JSON Patch.

## JSON-schema

JSON-schema är ett format som används för att beskriva och validera JSON-datastrukturen. [Experience Data Model (XDM)](../xdm/home.md) utnyttjar JSON-schemafunktioner för att införa begränsningar i strukturen och formatet för inmatade kundupplevelsedata. Mer information om JSON-schema finns i den [officiella dokumentationen](https://json-schema.org/).

## Nästa steg

I det här dokumentet introducerades en del av de tekniker och syntaxer som används för att hantera JSON-baserade resurser för Experience Platform. Mer information om hur du arbetar med plattforms-API:er, inklusive bästa praxis och svar på vanliga frågor, finns i felsökningsguiden för [plattformen](troubleshooting.md).