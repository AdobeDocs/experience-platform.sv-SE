---
title: Fältgrupp för uppgraderingsdetaljschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen för uppgraderingsinformation.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# [!UICONTROL Upgrade Details] schemafältgrupp

[!UICONTROL Upgrade Details] är en standardgrupp för schemafält för den  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klass som används för att samla in information om en marknadsföringshändelse för en uppgradering, inklusive information om transaktionen och olika sätt som erbjudandet visades för en kund.

Fältgruppen innehåller ett enskilt fält av objekttyp, `upgrades`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för uppgraderingsinformation](../../images/field-groups/upgrade-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `upgradeImpressions` | Matris med [Impressions](../../data-types/impressions.md) | En matris som listar de inspelade avbildningarna (digitala vyer eller engagemang med uppgraderingserbjudandet) för kunden. |
| `upgradeTransaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för uppgraderingen. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
