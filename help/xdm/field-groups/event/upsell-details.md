---
title: Schemafältgrupp för merförsäljning
description: Det här dokumentet innehåller en översikt över schemafältgruppen Upsell Details.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# [!UICONTROL Upsell Details] schemafältgrupp

[!UICONTROL Upsell Details] är en standardgrupp för schemafält för den  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klass som används för att samla in information om en merförsäljning av en marknadsföringshändelse, inklusive information om transaktionen och de olika sätt som erbjudandet visades för en kund.

Fältgruppen innehåller ett enskilt fält av objekttyp, `upsells`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för merförsäljning](../../images/field-groups/upsell-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `upsellImpressions` | Matris med [Impressions](../../data-types/impressions.md) | En matris som listar de inspelade intrycken (digitala vyer eller engagemang med merförsäljningserbjudandet) för kunden. |
| `upsellTransaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för merförsäljningen. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
