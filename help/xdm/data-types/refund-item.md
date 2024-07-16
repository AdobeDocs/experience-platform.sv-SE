---
title: Datatyp för återbetalningsartikel
description: Läs mer om datatypen XDM (Refund Item Experience Data Model).
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Datatypen [!UICONTROL Refund Item]

[!UICONTROL Refund Item] är en XDM-datatyp (Standard Experience Data Model) som beskriver samlar in information som är relaterad till en återbetalning som är kopplad till en order.

![Ett diagram över datatypen Återbetalningsartiklar.](../images/data-types/refund-item.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL Transaction ID] | `transactionID` | string | Unik transaktionsidentifierare för den här återbetalningsartikeln. |
| [!UICONTROL Refund Amount] | `refundAmount` | tal | Återbetalningsvärdet. |
| [!UICONTROL Refund Reason] | `refundReason` | string | Orsaken till varför en återbetalning utfärdades. |
| [!UICONTROL Refund Payment Type] | `refundPaymentType` | string | Betalningsmetoden för den här ordern. Anpassade värden är tillåtna. |
| [!UICONTROL Currency Code] | `currencyCode` | string | ISO 4217-valutakoden som används för den här återbetalningsartikeln. Exempel: USD, EUR. |

{style="table-layout:auto"}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
