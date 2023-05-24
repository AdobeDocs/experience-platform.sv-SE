---
title: Datatyp för finansiellt konto
description: Det här dokumentet innehåller en översikt över datatypen XDM för det finansiella kontot.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 1%

---

# [!UICONTROL Financial Account] datatyp

[!UICONTROL Financial Account] är en standard-XDM-datatyp som beskriver information om ett finansiellt konto, inklusive typ, ägare och aktuellt saldo.

![](../images/data-types/financial-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Currency]](./currency.md) | Kontots aktuella saldo. |
| `financialAccountId` | [!UICONTROL String] | Ett unikt ID för kontot. |
| `financialAccountName` | [!UICONTROL String] | Namnet som tilldelats kontot. |
| `financialAccountType` | [!UICONTROL String] | Typ av konto, t.ex. kontroll, sparande eller återlösen. |

{style="table-layout:auto"}

Mer information om datatypen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
