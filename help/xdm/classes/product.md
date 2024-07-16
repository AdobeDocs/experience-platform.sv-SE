---
title: Produktklass
description: Läs mer om produktklassen i Experience Data Model (XDM).
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# klassen [!UICONTROL Product]

I Experience Data Model (XDM) hämtar klassen [!UICONTROL Product] den minsta uppsättningen egenskaper som definierar en återförsäljningsprodukt.

![](../images/classes/product.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `productListPrice` | [Valuta](../data-types/currency.md) | Beskriver standardpriset för produkten före försäljning och rabatter. |
| `_id` | Sträng | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet är systemgenererat anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `productDescription` | Sträng | En beskrivning av produkten. |
| `productID` | Sträng | En unik identifierare för produkten. |
| `productLastModifiedDate` | DateTime | En [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339)-tidsstämpel som anger när den här produkten senast ändrades för uppdateringar. |
| `productManufacturedDate` | DateTime | En [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339)-tidsstämpel som anger när den här produkten skapades. |
| `productName` | Sträng | Produktens namn. |
| `productRating` | Sträng | Produktens kundrecensionsbetyg. |

{style="table-layout:auto"}

## Kompatibla fältgrupper {#field-groups}

Adobe tillhandahåller flera standardfältgrupper som kan användas med klassen [!UICONTROL Product]. Nedan följer en lista över några vanliga fältgrupper för klassen:

* [[!UICONTROL Product catalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Product category]](../field-groups/product/product-category.md)
