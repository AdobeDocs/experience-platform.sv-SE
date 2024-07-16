---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;scheman;adress;xdm:address;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Artikeldatatyp för produktlista
description: Läs mer om XDM-datatypen för produktlistobjektet.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Datatypen [!UICONTROL Product list item]

[!UICONTROL Product list item] är en standard-XDM-datatyp som beskriver en produkt som valts ut av en kund med specifika alternativ, priser och användningssammanhang för en viss tidpunkt.

De värden som registreras i den här datatypen kan skilja sig från produktposten. Produktposten innehåller till exempel uppgifter från produktinformationssystemet som är enhetliga för alla kunder, där produktlistartikeln har det faktiska pris som kunden erbjuds vid köptillfället, vilket kan variera beroende på försäljningskampanjer eller säsongspriser.

![](../images/data-types/product-list-item.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `selectedOptions` | Array med objekt | Innehåller anpassade alternativ som valts för en konfigurerbar produkt. Varje listobjekt är ett objekt med följande egenskaper:<ul><li>`attribute`: Ett namn för det konfigurerbara attributet.</li><li>`value`: Attributets värde.</li></ul> |
| `SKU` | [!UICONTROL String] | Lagerhållningsenhet (SKU), den unika identifieraren för en produkt som definieras av leverantören. |
| `_id` | [!UICONTROL String] | Identifierare för radartikel för den här produktposten. Själva produkten identifieras via `product`. |
| `currencyCode` | [!UICONTROL String] | Den alfabetiska valutakod [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) som används för att prissätta produkten. |
| `discountAmount` | [!UICONTROL Double] | Om produkten diskonteras motsvarar detta skillnaden mellan det ordinarie priset och specialpriset för produkten. |
| `name` | [!UICONTROL String] | Visningsnamnet för produkten som det visas för användaren för den här produktvyn. |
| `priceTotal` | [!UICONTROL Double] | Det totala priset för produktartikeln. |
| `product` | [!UICONTROL String] (URI) | URI `$id` för XDM-schemat som hämtar själva produkten. |
| `productAddMethod` | [!UICONTROL String] | Den metod som användes för att lägga till en produktartikel i listan av besökaren. |
| `productImageUrl` | [!UICONTROL String] | En URL för produktens huvudbild. |
| `quantity` | [!UICONTROL Integer] | Antalet enheter som kunden har angett att de behöver av produkten. |
| `unitOfMeasureCode` | [!UICONTROL String] | Standardmåttenheten [för produkten ](https://ucum.org/ucum) som är relaterad till egenskapen `quantity`. |

{style="table-layout:auto"}

Mer information om datatypen för postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
