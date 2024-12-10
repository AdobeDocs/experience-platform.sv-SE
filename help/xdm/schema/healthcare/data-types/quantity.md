---
title: Kvantitetsdatatyp
description: Läs mer om datatypen XDM (Quantity Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Datatypen [!UICONTROL Quantity]

[!UICONTROL Quantity] är en XDM-datatyp (Standard Experience Data Model) som ger en mätt eller mätbar mängd. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypstruktur för kvantitet](../../../images/healthcare/data-types/quantity.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Sträng | Enhetens kodade form. |
| [!UICONTROL Comparator] | `comparator` | Sträng | Jämförelseoperatorn. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL System] | `system` | Sträng | Det system som definierar det kodade enhetsformuläret, som representeras av en URI. |
| [!UICONTROL Unit] | `unit` | Sträng | Enhetsrepresentationen. |
| [!UICONTROL Value] | `value` | Dubbel | Det numeriska värdet. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
