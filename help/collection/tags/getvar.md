---
title: getVar()
description: Returnerar ett värde för ett dataelement eller en värdeuppsättning med setVar().
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# `getVar()`

Metoden `_satellite.getVar()` returnerar det aktuella värdet för ett [Data-element](/help/tags/ui/managing-resources/data-elements.md) eller en värdeuppsättning som använder [`_satellite.setVar()`](setvar.md). Om ett dataelement och ett `setVar()`-värde har samma namn, har dataelementet företräde. Om du anropar en strängidentifierare som inte finns än returnerar metoden `undefined`. Utvärderingen är synkron.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

Returvärdet och -typen beror på vilken dataelementtyp du refererar till. Om du till exempel anropar `getVar()` som hämtar en strängvariabel, returneras typen `string`. Om du anropar `getVar()` som returnerar ett dataelement från en Web SDK-variabel, är den returnerade typen en `object` som innehåller alla egenskaper som angetts i variabeln.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Tillgängliga fält

Metoden `getVar()` stöder två argument. De flesta fall innehåller inte det andra valfria argumentet.

| Namn | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| **`name`** | `string` | Ja | Det dataelementnamn som du vill hämta. Dataelementnamn är skiftlägeskänsliga. |
| **`event`** | `object` | Nej | Händelsekontext från den utlösande regeln. Används endast i avancerade fall av dataelement som använder [anpassad kod](/help/tags/ui/managing-resources/data-elements.md#custom-code) eller anpassade tillägg. När en regel utlöses av en händelse (t.ex. ett klick, en formulärsändning eller en anpassad utsändning från JavaScript), inkluderas det associerade händelseobjektet här. Dataelement kan använda den här informationen för att returnera sammanhangsberoende värden, till exempel information om det element som klickades eller egenskaper från en anpassad händelse. |
