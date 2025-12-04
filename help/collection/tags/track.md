---
title: track()
description: Utlös en regel för direktsamtal.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# `track()`

Med metoden `_satellite.track()` kan du utlösa en [regel för direktanrop](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>Adobe anser att `_satellite.track()` är en **äldre implementeringsmetod**. Även om det fortfarande stöds fullt ut rekommenderar Adobe starkt att du använder mer moderna implementeringsmetoder, till exempel [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md), vilket är den rekommenderade metoden för nya implementeringar.
>
>Om du väljer att använda `_satellite.track()` på din webbplats **skyddar du alla samtal** så att din webbplats inte är nära kopplad till taggbiblioteket. Om taggegenskapen inte är skyddad kommer alla referenser till `_satellite`-objektet att orsaka fel om du tar bort den i framtiden.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

När du anropar `_satellite.track()` med den identifierare som konfigurerats i tagggränssnittet aktiveras regeln omedelbart. Anrop av den här metoden fungerar bara som regelhändelse. Regelens villkor gäller fortfarande innan regelns åtgärder körs. Flera direktanropsregler kan använda samma identifierare, vilket gör att du kan utlösa alla dessa regler samtidigt med ett enda `_satellite.track()`-anrop. Varje utlöst regel kontrollerar fortfarande sina egna villkor innan den vidtar åtgärder, även om flera regler delar samma identifierare.

## Tillgängliga fält

Metoden `_satellite.track()` har stöd för två argument:

| Namn | Typ | Obligatoriskt | Beskrivning |
|---|---|---|---|
| **`identifier`** | `string` | Ja | Regelidentifieraren för direktanrop. Du anger den här identifieraren när du konfigurerar regeln i tagggränssnittet. |
| **`detail`** | `unknown` | Nej | En valfri nyttolast som innehåller önskad information. När du konfigurerar en regel kan du komma åt nyttolasten med `event.detail` (anpassad kod) eller `%event.detail%` (textfält som stöder dataelementsnotation). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
