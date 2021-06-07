---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Fältgrupp för Commerce Details
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen Commerce Details.
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---


# [!UICONTROL Commerce Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Commerce Details] är en standardgrupp för schemafält för  [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md), som används för att beskriva affärsdata som produktinformation (SKU, namn, kvantitet) och standardkundvagnsåtgärder (order, utcheckning, övergivna).

![](../../images/field-groups/commerce-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `commerce` | [Handel](../../data-types/commerce.md) | Ett objekt som beskriver produktreturer, garantiregistrering och kundvagns-/orderprocesser. |
| `productListItems` | Matris med [listobjekt](../../data-types/product-list-item.md) | En lista med artiklar som representerar den eller de produkter som kunden har valt, med specifika alternativ och priser vid en viss tidpunkt (som kan skilja sig från produktposten). |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-commerce.schema.json)
