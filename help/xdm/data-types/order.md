---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;ordning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Orderdatatyp
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM (Order Experience Data Model).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '182'
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

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)