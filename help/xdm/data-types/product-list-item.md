---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;scheman;adress;xdm:address;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Artikeldatatyp för produktlista
description: Det här dokumentet innehåller en översikt över XDM-datatypen för produktlistobjektet.
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# [!UICONTROL Product list item] datatyp

[!UICONTROL Product list item] är en standard-XDM-datatyp som beskriver en produkt som valts ut av en kund med specifika alternativ, priser och användningssammanhang för en viss tidpunkt.

De värden som registreras i den här datatypen kan skilja sig från produktposten. Produktposten innehåller till exempel uppgifter från produktinformationssystemet som är enhetliga för alla kunder, där produktlistartikeln har det faktiska pris som kunden erbjuds vid köptillfället, vilket kan variera beroende på försäljningskampanjer eller säsongspriser.

![](../images/data-types/product-list-item.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `selectedOptions` | Array med objekt | Innehåller anpassade alternativ som valts för en konfigurerbar produkt. Varje listobjekt är ett objekt med följande egenskaper:<ul><li>`attribute`: Ett namn för det konfigurerbara attributet.</li><li>`value`: Attributets värde.</li></ul> |
| `SKU` | [!UICONTROL String] | Lagerhållningsenhet (SKU), den unika identifieraren för en produkt som definieras av leverantören. |
| `_id` | [!UICONTROL String] | Identifierare för radartikel för den här produktposten. Själva produkten identifieras genom `product`. |
| `currencyCode` | [!UICONTROL String] | The [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) alfabetisk valutakod som används för att prissätta produkten. |
| `discountAmount` | [!UICONTROL Double] | Om produkten diskonteras motsvarar detta skillnaden mellan det ordinarie priset och specialpriset för produkten. |
| `name` | [!UICONTROL String] | Visningsnamnet för produkten som det visas för användaren för den här produktvyn. |
| `priceTotal` | [!UICONTROL Double] | Det totala priset för produktartikeln. |
| `product` | [!UICONTROL String] (URI) | URI `$id` av XDM-schemat som hämtar själva produkten. |
| `productAddMethod` | [!UICONTROL String] | Den metod som användes för att lägga till en produktartikel i listan av besökaren. |
| `productImageUrl` | [!UICONTROL String] | En URL för produktens huvudbild. |
| `quantity` | [!UICONTROL Integer] | Antalet enheter som kunden har angett att de behöver av produkten. |
| `unitOfMeasureCode` | [!UICONTROL String] | Standarden [måttenhetskod](https://ucum.org/ucum) för produkten i fråga `quantity` -egenskap. |

{style="table-layout:auto"}

Mer information om datatypen för postadresser finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
