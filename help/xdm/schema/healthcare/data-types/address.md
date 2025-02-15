---
title: Adressdatatyp
description: Läs mer om datatypen XDM (Address Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Datatypen [!UICONTROL Address]

[!UICONTROL Address] är en XDM-datatyp (Standard Experience Data Model) som beskriver en adress som uttrycks med hjälp av postkonventioner (till skillnad från GPS eller andra platsdefinitionsformat). Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Adressdatatypstruktur](../../../images/healthcare/data-types/address.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Tidsperiod då adressen användes/används. |
| [!UICONTROL City] | `city` | Sträng | Ortens namn. |
| [!UICONTROL Country] | `country` | Sträng | Den landskod som beskrivs i den internationella standarden ISO 3166. Koden kan vara antingen alfa-2 eller alfa-3. |
| [!UICONTROL District] | `district` | Sträng | Distriktets namn. |
| [!UICONTROL Line] | `line` | Sträng | Gatunamn, nummer, riktning, postbox eller liknande. |
| [!UICONTROL Postal Code] | `postalCode` | Sträng | Postnumret. |
| [!UICONTROL State] | `state` | Sträng | Underenheten för ett land. Förkortningar är acceptabla. |
| [!UICONTROL Text] | `text` | Sträng | Adressens textbeteckning. |
| [!UICONTROL Type] | `type` | Sträng | Adresstypen. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Use] | `use` | Sträng | Adressens syfte. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
