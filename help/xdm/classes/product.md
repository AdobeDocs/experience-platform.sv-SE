---
title: Product Class
description: This document provides an overview of the Product class in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---

# [!UICONTROL Product]

[!UICONTROL Product]

![](../images/classes/product.png)

| Property | Data type | Beskrivning |
| --- | --- | --- |
| `productListPrice` | [](../data-types/currency.md) | Describes the default price of the product before sales and discounting. |
| `_id` | Sträng | A unique, system-generated string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and to look up that record in downstream services.<br><br> However, you can still opt to supply your own unique ID values if you wish. |
| `productDescription` | Sträng | A description of the product. |
| `productID` | Sträng | A unique identifier for the product. |
| `productLastModifiedDate` | DateTime | [](https://datatracker.ietf.org/doc/html/rfc3339) |
| `productManufacturedDate` | DateTime | [](https://datatracker.ietf.org/doc/html/rfc3339) |
| `productName` | Sträng | The name of the product. |
| `productRating` | Sträng | The customer review rating of the product. |

{style=&quot;table-layout:auto&quot;}

## Compatible field groups {#field-groups}

[!DNL XDM Individual Profile] The following is a list of some commonly used field groups for the class:

* [[!UICONTROL Product catalog]](../field-groups/product/product-catalog.md)
* [[!UICONTROL Product category]](../field-groups/product/product-category.md)
