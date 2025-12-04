---
title: setVar()
description: Anger ett värde som du kan hämta senare med getVar().
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# `setVar()`

Med metoden `_satellite.setVar()` kan du ange ett eller flera anpassade namn/värde-par som senare kan refereras av [`_satellite.getVar()`](getvar.md).

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Metoden `getVar()` kan hämta både dataelement och värden som anges av `setVar()`, men dessa två entitetstyper är separata. Om du använder `setVar()` för att ange ett värde med samma namn som ett dataelement i tagggränssnittet skrivs det inte över.

## Beständighet och omfång

`setVar()` värden finns bara i sidminnet:

* **Endast aktuell sida**: Värdena kvarstår tills sidan har tagits bort. I enkelsidiga program kvarstår de tills en fullständig inläsning eller du skriver över/rensar dem.
* **Ingen webbläsarlagring**: Inget skrivs till cookies, lokal lagring eller sessionslagring.

## Refererar till värden som angetts med `setVar()`

Du kan hämta värden i anpassad kod med `getVar()`:

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

Du kan också referera till dessa variabler i tagggränssnittet i fält som har stöd för dataelementsnotation:

```text
%Ad location%
```

>[!NOTE]
>
>Om en värdeuppsättning som använder `setVar()` använder samma namn som ett dataelement och du refererar till det namnet i dataelementnotationen, har dataelementet företräde.

## Exempel

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```
