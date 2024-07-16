---
title: Fältgrupp för insättningsdetaljschema
description: Läs mer om schemafältgruppen Insättningsinformation.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 1%

---

# Schemafältgruppen [!UICONTROL Deposit Details]

[!UICONTROL Deposit Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md). Fältgruppen tillhandahåller ett enskilt `personalFinances.deposits`-fält till ett schema, som samlar in information om en finansiell insättning.

![](../../images/field-groups/deposit-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `account` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beskriver det finansiella konto som är associerat med insättningen. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beskriver den finansiella transaktion som är associerad med insättningen. |
| `mobileDeposit` | [!UICONTROL Boolean] | Anger om insättningen gjordes via en mobilplattform. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
