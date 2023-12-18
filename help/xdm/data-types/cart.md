---
title: Kunddatatyp
description: Läs mer om datatypen Cart Experience Data Model (XDM).
source-git-commit: c3590dc2cfe47eb634136eeb88578f965598760d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# [!UICONTROL Cart] datatyp

[!UICONTROL Cart] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller egenskaper för en kundvagn. Använd den här datatypen för att hämta den unika identifieraren som tilldelats av säljaren (`Cart ID`) och källan (`Cart Source`) där en eller flera produkter har tillsatts i varukorgen.

![Ett diagram över [!UICONTROL Cart] datatyp.](../images/data-types/cart.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Cart ID] | `cartID` | string | Unik identifierare som tilldelats av säljaren för kundvagnen. |
| [!UICONTROL Cart Source] | `cartSource` | string | Om en eller flera produkter har lagts till i varukorgen. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
