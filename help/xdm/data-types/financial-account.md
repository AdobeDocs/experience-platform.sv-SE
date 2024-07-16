---
title: Datatyp för finansiellt konto
description: Läs mer om datatypen XDM för det finansiella kontot.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

---

# Datatypen [!UICONTROL Financial Account]

[!UICONTROL Financial Account] är en standard-XDM-datatyp som beskriver informationen för ett finansiellt konto, inklusive typ, ägare och aktuellt saldo.

![](../images/data-types/financial-account.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Currency]](./currency.md) | Kontots aktuella saldo. |
| `financialAccountId` | [!UICONTROL String] | Ett unikt ID för kontot. |
| `financialAccountName` | [!UICONTROL String] | Namnet som tilldelats kontot. |
| `financialAccountType` | [!UICONTROL String] | Typ av konto, t.ex. kontroll, sparande eller återlösen. |

{style="table-layout:auto"}

Mer information om datatypen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
