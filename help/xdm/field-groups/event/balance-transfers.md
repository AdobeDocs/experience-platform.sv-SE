---
title: Balansöverföringar schemafältgrupp
description: Läs mer om schemafältgruppen Balansöverföringar.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# [!UICONTROL Balance Transfers] schemafältgrupp

[!UICONTROL Balance Transfers] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `personalFinances.balanceTransfers` objekt till ett schema, som innehåller information om en överföring av ett ekonomiskt saldo mellan konton.

![](../../images/field-groups/balance-transfers.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beskriver det finansiella konto som saldot överförs från. |
| `accountTo` | [[!UICONTROL Financial Account]](../../data-types/financial-account.md) | Beskriver det finansiella konto som saldot överförs till. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | Beskriver den finansiella transaktion som är associerad med saldoöverföringen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
