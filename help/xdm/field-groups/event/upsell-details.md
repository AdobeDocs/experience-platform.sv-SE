---
title: Schemafältgrupp för merförsäljning
description: Det här dokumentet innehåller en översikt över schemafältgruppen Upsell Details.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# [!UICONTROL Upsell Details] schemafältgrupp

[!UICONTROL Upsell Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) som används för att samla in information om ett marknadsföringsevenemang med merförsäljning, inklusive information om transaktionen och olika sätt som erbjudandet visades för en kund.

Fältgruppen innehåller ett enda fält av objekttyp, `upsells`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för merförsäljning](../../images/field-groups/upsell-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `upsellImpressions` | Array med [Impressions](../../data-types/impressions.md) | En matris som listar de inspelade intrycken (digitala vyer eller engagemang med merförsäljningserbjudandet) för kunden. |
| `upsellTransaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för merförsäljningen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
