---
title: Fältgrupp för uppgraderingsdetaljschema
description: Läs mer om schemafältgruppen Uppgraderingsinformation.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# [!UICONTROL Upgrade Details] schemafältgrupp

[!UICONTROL Upgrade Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) används för att samla in information om ett uppgraderingsevenemang, inklusive information om transaktionen och olika sätt som erbjudandet visades för en kund.

Fältgruppen innehåller ett enda fält av objekttyp, `upgrades`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för uppgraderingsinformation](../../images/field-groups/upgrade-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `upgradeImpressions` | Array med [Impressions](../../data-types/impressions.md) | En matris som listar de inspelade avbildningarna (digitala vyer eller engagemang med uppgraderingserbjudandet) för kunden. |
| `upgradeTransaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för uppgraderingen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
