---
title: Typ av rapportering av data för anpassad metadatainformation
description: Läs mer om datatypen XDM (Custom Metadata Details Reporting Experience Data Model).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Datatypen [!UICONTROL Custom Metadata Details] för rapportering

[!UICONTROL Custom Metadata Details]-rapportering är en XDM-datatyp (Standard Experience Data Model) som definierar en struktur för lagring av anpassade metadata. Datatypen [!UICONTROL Custom Metadata Details] Reporting samlar in information som namn och värde på anpassade metadata som är associerade med innehåll eller interaktioner. Medierapporteringsfält används av Adobe-tjänster för att analysera de mediesamlingsfält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån.

![Ett diagram över datatypen Custom Metadata Details Reporting.](../images/data-types/the-custom-metadata-reporting.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Namnet på det anpassade fältet. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Värdet för det anpassade fältet. |

{style="table-layout:auto"}
