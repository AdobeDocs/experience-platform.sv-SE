---
title: Datatyp för insamling av anpassad metadatainformation
description: Läs mer om datatypen XDM (Custom Metadata Details Collection Experience Data Model).
exl-id: e2fa65ea-b738-43c6-90f1-1968dd83b963
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 1%

---

# [!UICONTROL Custom Metadata Details] Samlingsdatatyp

[!UICONTROL Custom Metadata Details]-samlingen är en XDM-datatyp (Standard Experience Data Model) som definierar en struktur för lagring av anpassade metadata. Använd datatypen [!UICONTROL Custom Metadata Details] Samling för att samla in information som namn och värde på anpassade metadata som är associerade med innehåll eller interaktioner.

![Ett diagram med datatypen Custom Metadata Details Collection.](../images/data-types/the-custom-metadata-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|--------------------------------------------|------------------|-----------|----------|-------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Nej | Namnet på det anpassade fältet. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Nej | Värdet för det anpassade fältet. |

{style="table-layout:auto"}
