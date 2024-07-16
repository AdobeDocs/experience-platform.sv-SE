---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;field group;
solution: Experience Platform
title: Commerce Details Schema Field Group
description: Läs mer om schemafältgruppen Commerce Details.
exl-id: 36aba186-fadb-4abb-a94f-7e151ff3f744
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Commerce Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Commerce Details] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md) som används för att beskriva handelsdata, t.ex. produktinformation (SKU, namn, kvantitet) och standardkundvagnsåtgärder (beställning, utcheckning, övergivna).

![](../../images/field-groups/commerce-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `commerce` | [Commerce](../../data-types/commerce.md) | Ett objekt som beskriver produktreturer, garantiregistrering och kundvagns-/orderprocesser. |
| `productListItems` | Matris med [listobjekt](../../data-types/product-list-item.md) | En lista med artiklar som representerar den eller de produkter som kunden har valt, med specifika alternativ och priser vid en viss tidpunkt (som kan skilja sig från produktposten). |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json)
