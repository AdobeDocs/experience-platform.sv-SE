---
title: Produktklass
description: Det här dokumentet innehåller en översikt över produktklassen i Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 2%

---

# [!UICONTROL Product] class

I Experience Data Model (XDM) är [!UICONTROL Product] klassen hämtar den minsta uppsättningen egenskaper som definierar en återförsäljningsprodukt.

![](../images/classes/product.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Beskriver standardpriset för produkten före försäljning och rabatter. |
| `_id` | Sträng | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `productDescription` | Sträng | En beskrivning av produkten. |
| `productID` | Sträng | En unik identifierare för produkten. |
| `productLastModifiedDate` | DateTime | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) tidsstämpel för när produkten senast ändrades för uppdateringar. |
| `productManufacturedDate` | DateTime | An [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) tidsstämpel för när den här produkten skapades. |
| `productName` | Sträng | Produktens namn. |
| `productRating` | Sträng | Kundens recensionsbedömning av produkten. |

{style=&quot;table-layout:auto&quot;}

## Kompatibla fältgrupper {#field-groups}

Adobe har flera standardfältgrupper som kan användas med [!UICONTROL Product] klassen. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL Product catalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Product category]](../field-groups/product/product-category.md)
