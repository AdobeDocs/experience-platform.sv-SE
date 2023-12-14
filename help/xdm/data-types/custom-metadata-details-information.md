---
title: Datatyp för anpassad metadatainformation
description: Läs mer om datatypen XDM (Custom Metadata Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# [!UICONTROL Custom Metadata Details Information] datatyp

[!UICONTROL Custom Metadata Details Information] är en XDM-datatyp (Standard Experience Data Model) som definierar en struktur för lagring av anpassade metadata. Använd [!UICONTROL Custom Metadata Details Information] datatyp för att samla in information som namn och värde på anpassade metadata som är associerade med innehåll eller interaktioner.

![Ett diagram över datatypen Custom Metadata Details.](../images/data-types/custom-metadata-details-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Namnet på det anpassade fältet. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Värdet för det anpassade fältet. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
