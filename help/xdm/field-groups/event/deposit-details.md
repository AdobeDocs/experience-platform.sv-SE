---
title: Fältgrupp för insättningsdetaljschema
description: Läs mer om schemafältgruppen Insättningsinformation.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# [!UICONTROL Deposit Details] schemafältgrupp

[!UICONTROL Deposit Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `personalFinances.deposits` till ett schema, som innehåller information om en finansiell insättning.

![](../../images/field-groups/deposit-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `account` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beskriver det finansiella konto som är associerat med insättningen. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beskriver den finansiella transaktion som är associerad med insättningen. |
| `mobileDeposit` | [!UICONTROL Boolean] | Anger om insättningen gjordes via en mobilplattform. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
