---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;ordning;datatyp;datatyp;datatyp;data type;
solution: Experience Platform
title: Orderdatatyp
description: Läs mer om datatypen XDM (Order Experience Data Model).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# [!UICONTROL Order] datatyp

[!UICONTROL Order] är en XDM-datatyp (Standard Experience Data Model) som beskriver den ordning som används för en produktlista.

![Ett diagram över [!UICONTROL Order] datatyp.](../images/data-types/order.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Inköps-ID | `purchaseID` | Sträng | En unik identifierare som säljaren har tilldelat detta inköp eller kontrakt. Det finns ingen garanti för att ID:t är unikt eftersom ID:t definieras av säljaren. |
| Inköpsordernummer | `purchaseOrderNumber` | Sträng | En unik identifierare som tilldelats av köparen för detta inköp eller kontrakt. |
| Betalningslista | `payments` | Array med [[!UICONTROL Payment Items]](./payment-item.md) | Listan över betalningar för den här ordern. Betalningarna beskrivs i [!UICONTROL Payment Items] -specifikation. |
| Återbetalningslista | `refunds` | Array med [[!UICONTROL Refund Items]](./refund-item.md) | Listan över återbetalningar för den här ordern. Bidragen anges i [!UICONTROL Refund Items] -specifikation. |
| Returinfo | `returns` | [[!UICONTROL Return Info]](./return.md) | RMA (Return Merchandise Authorization) har utfärdats. Returerna anges i [!UICONTROL Return Info] -specifikation. |
| Valuta | `currencyCode` | Sträng | ISO 4217-valutakoden som används för ordersummor. Exempel: `USD` och `EUR`. Alla instanser måste matcha mönstret `^[A-Z]{3}$`. |
| Momsbelopp | `taxAmount` | Nummer | Det skattebelopp som köparen betalar som en del av den slutliga betalningen. |
| Rabattbelopp | `discountAmount` | Nummer | Skillnaden mellan normalpriset och specialpriset för hela ordern, i stället för enskilda produkter. |
| Prissumma | `priceTotal` | Nummer | Det totala priset för den här ordern efter att alla rabatter och skatter har tillämpats. |
| Ordertyp | `orderType` | Sträng | Den typ av order som har placerats ut. Möjliga värden är `checkout` och `instant_purchase`. |
| Senast uppdaterat | `lastUpdatedDate` | Sträng | Den tidpunkt då en viss orderpost senast uppdaterades i handelssystemet. Format: datum-tid. |
| Skapad den | `createdDate` | Sträng | Den tid/det datum då en ny order skapas i handelssystemet. Format: datum-tid. |
| Annullera datum | `cancelDate` | Sträng | Det datum/den tidpunkt då kunden initierade en annullering av en order. Format: datum-tid. |
| Totalt återgivet belopp | `refundTotal` | Nummer | Det totala belopp som anges i denna återbetalning för ordern, med kombination av alla återfinansierade artiklar och efter eventuella rabatter osv. har tillämpats. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
