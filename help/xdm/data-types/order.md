---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;ordning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Orderdatatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM (Order Experience Data Model).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# [!UICONTROL Order] datatyp

[!UICONTROL Order] är en XDM-datatyp (Standard Experience Data Model) som beskriver den ordning som används för en produktlista.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `payments` | Matris med [[!UICONTROL Payment Items]](./payment-item.md) | Listan över betalningar för den här ordern. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som används för ordersummor. Alla instanser måste överensstämma med det reguljära uttrycket `^[A-Z]{3}$`. Exempel är `USD` och `EUR`. |
| `priceTotal` | Dubbel | Det totala priset för den här ordern efter att alla rabatter och skatter har tillämpats. |
| `purchaseID` | Sträng | En unik identifierare som säljaren har tilldelat detta inköp eller kontrakt. Eftersom detta definieras av säljaren finns det ingen garanti för att ID:t är unikt. |
| `purchaseOrderNumber` | Sträng | Den unika identifierare som tilldelats av köparen för detta inköp eller kontrakt. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
