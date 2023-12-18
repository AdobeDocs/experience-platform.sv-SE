---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;ordning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Orderdatatyp
description: Läs mer om datatypen XDM (Order Experience Data Model).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# [!UICONTROL Order] datatyp

[!UICONTROL Order] är en XDM-datatyp (Standard Experience Data Model) som beskriver den ordning som används för en produktlista.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `payments` | Array med [[!UICONTROL Payment Items]](./payment-item.md) | Listan över betalningar för den här ordern. |
| `currencyCode` | Sträng | ISO 4217-valutakoden som används för ordersummor. Alla instanser måste överensstämma med det reguljära uttrycket `^[A-Z]{3}$`. Exempel: `USD` och `EUR`. |
| `priceTotal` | Dubbel | Det totala priset för den här ordern efter att alla rabatter och skatter har tillämpats. |
| `purchaseID` | Sträng | En unik identifierare som säljaren har tilldelat detta inköp eller kontrakt. Eftersom detta definieras av säljaren finns det ingen garanti för att ID:t är unikt. |
| `purchaseOrderNumber` | Sträng | Den unika identifierare som tilldelats av köparen för detta inköp eller kontrakt. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
