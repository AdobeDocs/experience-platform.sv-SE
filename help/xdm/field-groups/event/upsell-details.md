---
title: Schemafältgrupp för merförsäljning
description: Läs mer om schemafältgruppen Upsell Details.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Upsell Details]

[!UICONTROL Upsell Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att samla in information om en marknadsföringshändelse för merförsäljning, inklusive information om transaktionen och olika sätt som erbjudandet visades för en kund.

Fältgruppen innehåller ett enskilt fält av objekttyp, `upsells`. Egenskaperna i det här objektet förklaras nedan.

![Struktur för merförsäljningsinformation](../../images/field-groups/upsell-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `upsellImpressions` | Matris med [Impressions](../../data-types/impressions.md) | En matris som listar de inspelade intrycken (digitala vyer eller engagemang med merförsäljningserbjudandet) för kunden. |
| `upsellTransaction` | [Transaktion](../../data-types/transaction.md) | Beskriver valutatransaktionen för merförsäljningen. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
