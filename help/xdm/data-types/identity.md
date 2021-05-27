---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;Schemas;identity;datatype;data type;data type;
solution: Experience Platform
title: Identitetsdatatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen Identity XDM.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# [!UICONTROL Identity] datatyp

[!UICONTROL Identity] är en standard-XDM-datatyp som används för att tydligt skilja människor som interagerar med digitala upplevelser åt. Identiteten etableras av en identitetsleverantör, som själv refereras i ett `namespace`-attribut. I varje `namespace` är identiteten unik.

<img src="../images/data-types/identity.png" width="550" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `namespace` | Objekt | Ett objekt som innehåller ett strängfält (`code`), som anger det namnutrymme som är associerat med det angivna `id`-attributet. |
| `authenticatedState` | Sträng | Det autentiserade tillståndet för den här identiteten vid tidpunkten för den observerade Experience-händelsen. Se [bilagan](#authenticatedState) för godkända värden och definitioner. |
| `id` | Sträng | Identiteten för konsumenten i det relaterade namnutrymmet. |
| `primary` | Boolean | Anger om detta är den primära identiteten för den enskilda personen. Varje enskild person kan bara ha en primär identitet. |
| `xid` | Sträng | Om det finns en sådan representerar det här värdet en identifierare för korsnamnutrymme som är unik för alla identifierare som omfattar alla namnutrymmen i alla namnutrymmen. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Bilaga

Följande avsnitt innehåller ytterligare information om datatypen [!UICONTROL Identity].

## Godkända värden för authenticatedState {#authenticatedState}

I följande tabell visas godkända värden för `authenticatedState` och deras associerade betydelse:

| Värde | Beskrivning |
| --- | --- |
| `ambiguous` | Det autentiserade läget är tvetydigt. |
| `authenticated` | Användaren identifierades med en inloggning eller liknande åtgärd som var giltig vid tidpunkten för händelseobservationen. |
| `loggedOut` | Användaren identifierades av en inloggningsåtgärd vid en tidigare tidpunkt, men loggades inte in vid tidpunkten för händelseobservationen. |
