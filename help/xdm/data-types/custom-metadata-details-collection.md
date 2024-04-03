---
title: Datatyp för insamling av anpassad metadatainformation
description: Läs mer om datatypen XDM (Custom Metadata Details Collection Experience Data Model).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 1%

---

# [!UICONTROL Custom Metadata Details] Samlingsdatatyp

[!UICONTROL Custom Metadata Details] Samlingen är en XDM-datatyp (Experience Data Model) som definierar en struktur för lagring av anpassade metadata. Använd [!UICONTROL Custom Metadata Details] Samlingsdatatyp för att samla in information som namn och värde på anpassade metadata som är associerade med innehåll eller interaktioner.

![Ett diagram över datatypen Custom Metadata Details Collection.](../images/data-types/the-custom-metadata-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------------------|------------------|-----------|----------|-------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Nej | Namnet på det anpassade fältet. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Nej | Värdet för det anpassade fältet. |

{style="table-layout:auto"}
