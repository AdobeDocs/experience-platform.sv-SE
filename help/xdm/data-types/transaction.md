---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;transaktion;datatyp;datatyp;datatyp;data type;
title: Transaktionsdatatyp
description: Läs mer om datatypen XDM (Transaction Experience Data Model).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# Datatypen [!UICONTROL Transaction]

[!UICONTROL Transaction] är en XDM-datatyp (Standard Experience Data Model) som beskriver informationen för en monetär transaktion.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Currency]](./currency.md) | Beskriver beloppet för den valuta som byts ut som en del av transaktionen. |
| `transactionDate` | [!UICONTROL DateTime] | En tidsstämpel som anger när transaktionen utfördes. |
| `transactionId` | [!UICONTROL String] | En unik identifierare för transaktionen. |
| `transactionType` | [!UICONTROL String] | Den typ av transaktion som används av besökaren. |

{style="table-layout:auto"}
