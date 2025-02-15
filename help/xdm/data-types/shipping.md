---
title: Leveransdatatyp
description: Läs mer om datatypen XDM (Shipping Experience Data Model).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Datatypen [!UICONTROL Shipping]

[!UICONTROL Shipping] är en XDM-datatyp (Standard Experience Data Model) som ger information om leveransen av en eller flera produkter. Den innehåller information om logistik och information om leverans av beställda artiklar.


![Ett diagram över datatypen [!UICONTROL Shipping].](../images/data-types/shipping.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Shipping Method] | `shippingMethod` | string | Leveranssätt som kunden valt. |
| [!UICONTROL Shipping Amount] | `shippingAmount` | tal | Det belopp som kunden måste betala för frakt. |
| [!UICONTROL Currency code] | `currencyCode` | string | ISO 4217 alfabetisk valutakod som används för att prissätta produkten. |
| [!UICONTROL Shipping Destination] | `shippingDestination` | string | Det leveransmål som anges av användaren (till exempel home, store och så vidare). |
| [!UICONTROL Ship Date] | `shipDate` | string | Det datum då en eller flera artiklar från en order skickas. |
| [!UICONTROL Shipping Address] | `address` | [[!UICONTROL address]](./address.md) | Leveransadress. |
| [!UICONTROL Tracking Number] | `trackingNumber` | tal | Spårningsnumret som anges av transportföretaget. |
| [!UICONTROL Tracking URL] | `trackingURL` | string | URL:en som spårar leveransstatus för en orderartikel. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
