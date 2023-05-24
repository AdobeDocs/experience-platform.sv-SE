---
title: Fältgrupp för insättningsdetaljschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Insättningsinformation.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

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
