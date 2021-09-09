---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;transaktion;datatyp;datatyp;datatyp;data type;
title: Transaktionsdatatyp
description: Det här dokumentet innehåller en översikt över datatypen XDM (Transaction Experience Data Model).
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# [!UICONTROL Transaction] datatyp

[!UICONTROL Transaction] är en XDM-datatyp (Standard Experience Data Model) som beskriver detaljerna i en monetär transaktion.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Currency]](./currency.md) | Beskriver beloppet för den valuta som byts ut som en del av transaktionen. |
| `transactionDate` | [!UICONTROL DateTime] | En tidsstämpel som anger när transaktionen utfördes. |
| `transactionId` | [!UICONTROL String] | En unik identifierare för transaktionen. |
| `transactionType` | [!UICONTROL String] | Den typ av transaktion som används av besökaren. |

{style=&quot;table-layout:auto&quot;}
