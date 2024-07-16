---
title: Kunddatatyp
description: Läs mer om datatypen Cart Experience Data Model (XDM).
exl-id: 24ae3882-60f3-4962-b0b5-7dba48170da8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Datatypen [!UICONTROL Cart]

[!UICONTROL Cart] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller egenskaper som är relaterade till en kundvagn. Använd den här datatypen för att hämta den unika identifieraren som tilldelats av säljaren (`Cart ID`) och källan (`Cart Source`) där en eller flera produkter lades till i kundvagnen.

![Ett diagram över datatypen [!UICONTROL Cart].](../images/data-types/cart.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------|-------------------|-----------|------------------------------------------------------------|
| [!UICONTROL Cart ID] | `cartID` | string | Unik identifierare som tilldelats av säljaren för kundvagnen. |
| [!UICONTROL Cart Source] | `cartSource` | string | Om en eller flera produkter har lagts till i varukorgen. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json)
