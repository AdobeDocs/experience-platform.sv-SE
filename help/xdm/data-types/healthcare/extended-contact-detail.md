---
title: Datatyp för utökad kontaktinformation
description: Läs mer om datatypen XDM (Extended Contact Detail Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Datatypen [!UICONTROL Extended Contact Detail]

[!UICONTROL Extended Contact Detail] är en XDM-datatyp (Standard Experience Data Model) som beskriver informationen för en utökad kontakt. Den här datatypen skapas enligt specifikationerna för HL7 FHIR version 5.

![Struktur för datatypen Utökad kontaktinformation](../../images/data-types/healthcare/extended-contact-detail.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | [[!UICONTROL Address]](../healthcare/address.md) | Kontaktens adress. |
| [!UICONTROL Name] | `name` | Array med [[!UICONTROL Human Name]](../healthcare/human-name.md) | Namnet/namnen på personen/personerna som ska kontaktas. |
| [!UICONTROL Organization] | `organization` | [[!UICONTROL Reference]](../healthcare/reference.md) | Organisationen som hanterar/övervakar kontaktinformationen. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../healthcare/period.md) | Den period som kontakten är eller var giltig för användning. |
| [!UICONTROL Purpose] | `purpose` | [[!UICONTROL Codeable Concept]](../healthcare/codeable-concept.md) | Typ av kontakt. |
| [!UICONTROL Telecom] | `telecom` | Array med [[!UICONTROL Contact Point]](../healthcare/contact-point.md) | Kontaktinformationen. |

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/extendedcontactdetail.schema.json)
