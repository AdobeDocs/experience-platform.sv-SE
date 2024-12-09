---
title: Kontaktpunktens datatyp
description: Läs mer om datatypen XDM (Contact Point Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Datatypen [!UICONTROL Contact Point]

[!UICONTROL Contact Point] är en XDM-datatyp (Standard Experience Data Model) som beskriver en persons kontaktinformation. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Datatypstruktur för kontaktpunkt](../../images/data-types/healthcare/contact-point.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../healthcare/period.md) | Den tidsperiod då kontaktpunkten användes/används. |
| [!UICONTROL Rank] | `rank` | Heltal | Den rankning som anger kontaktpunktens önskade användning. Det lägsta värdet är `1` och det högsta värdet är `2147483647` där `1` är den högsta specificiteten. |
| [!UICONTROL System] | `system` | Sträng | Det system genom vilket de kan kontaktas. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL Use] | `use` | Sträng | Kontaktpunktens syfte. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL Value] | `value` | Sträng | Kontaktpunktens information. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)
