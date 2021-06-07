---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;scheman;adress;xdm:address;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Artikeldatatyp för produktlista
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över XDM-datatypen för produktlistobjektet.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# [!UICONTROL Product list item] datatyp

[!UICONTROL Product list item] är en standard-XDM-datatyp som beskriver en produkt som valts ut av en kund med specifika alternativ, priser och användningssammanhang för en viss tidpunkt.

De värden som registreras i den här datatypen kan skilja sig från produktposten. Produktposten innehåller till exempel uppgifter från produktinformationssystemet som är enhetliga för alla kunder, där produktlistartikeln har det faktiska pris som kunden erbjuds vid köptillfället, vilket kan variera beroende på försäljningskampanjer eller säsongspriser.

![](../images/data-types/product-list-item.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `SKU` | [!UICONTROL String] | Lagerhållningsenhet (SKU), den unika identifieraren för en produkt som definieras av leverantören. |
| `_id` | [!UICONTROL String] | Identifierare för radartikel för den här produktposten. Själva produkten identifieras med `product`. |
| `currencyCode` | [!UICONTROL String] | Den alfabetiska valutakod [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) som används för att prissätta produkten. |
| `name` | [!UICONTROL String] | Visningsnamnet för produkten som det visas för användaren för den här produktvyn. |
| `priceTotal` | [!UICONTROL Double] | Det totala priset för produktartikeln. |
| `product` | [!UICONTROL String] (URI) | URI `$id` för XDM-schemat som hämtar själva produkten. |
| `productAddMethod` | [!UICONTROL String] | Den metod som användes för att lägga till en produktartikel i listan av besökaren. |
| `quantity` | [!UICONTROL Integer] | Antalet enheter som kunden har angett att de behöver av produkten. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen för postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
