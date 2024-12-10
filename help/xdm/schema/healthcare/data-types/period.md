---
title: Datatyp för period
description: Läs mer om datatypen XDM (Period Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 1%

---

# Datatypen [!UICONTROL Period]

[!UICONTROL Period] är en XDM-datatyp (Standard Experience Data Model) som tillhandahåller en tidsperiod som definieras av ett start- och slutdatum/tid. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för perioddatatyp](../../../images/healthcare/data-types/period.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL End] | `end` | DateTime | Slutdatum och sluttid. |
| [!UICONTROL Start] | `start` | DateTime | Startdatum och starttid. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
