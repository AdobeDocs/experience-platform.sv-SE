---
title: Schemafältgrupp för offertförfrågningsinformation
description: Läs mer om schemafältgruppen Offertförfrågningsinformation.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# [!UICONTROL Quote Request Details] schemafältgrupp

[!UICONTROL Quote Request Details] är en standardgrupp för schemafält för [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Fältgruppen innehåller en `quotes` invänder mot ett schema som innehåller information om förfrågningsprocessen för olika typer av offerter, inklusive försäkringsbrev, hälso- och sjukvård, tillverkningsorder och hightech-order.

![](../../images/field-groups/quote-request-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `discount` | [[!UICONTROL Currency]](../../data-types/currency.md) | Rabattbeloppet för en offert som visas för en besökare. |
| `premium` | [[!UICONTROL Currency]](../../data-types/currency.md) | Premiumbeloppet för en offert som visas för en besökare. |
| `location` | [!UICONTROL String] | Postnumret som används för att hitta återförsäljare nära besökarens plats. |
| `requestID` | [!UICONTROL String] | En unik identifierare för offertförfrågan. |
| `selectedRetailer` | [!UICONTROL String] | Den valda återförsäljaren för anbudsförfrågan, om tillämpligt. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
