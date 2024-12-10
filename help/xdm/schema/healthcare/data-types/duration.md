---
title: Datatypen Varaktighet
description: Läs mer om datatypen XDM (Duration Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 01aac0d0-0503-4f8b-a306-cf3c187a76e0
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Datatypen [!UICONTROL Duration]

[!UICONTROL Duration] är en XDM-datatyp (Standard Experience Data Model) som beskriver en tidsperiod. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypsstruktur för varaktighet](../../../images/healthcare/data-types/duration.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Sträng | Den kodade formen av tidsenheten. |
| [!UICONTROL System] | `system` | Sträng | Det system som beskriver den kodade enheten, representerat som en URI. |
| [!UICONTROL Unit] | `unit` | Sträng | Tidsenheten i millisekunder, sekunder, minuter, timmar, dagar, veckor, månader eller år. Värdena för den här egenskapen måste vara lika med ett eller flera av följande kända enum-värden. <li> `ms` (millisekunder) </li> <li> `s` (sekunder) </li> <li> `min` (minuter) </li> <li> `h` (timmar) </li>  <li> `d` (dagar) </li> <li> `wk` (veckor) </li> <li> `mo` (månader) </li> <li> `a` (år) </li> |
| [!UICONTROL Value] | `value` | Dubbel | Det numeriska värdet för tidsenheten. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
