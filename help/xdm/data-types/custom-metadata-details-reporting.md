---
title: Typ av rapportering av data för anpassad metadatainformation
description: Läs mer om datatypen XDM (Custom Metadata Details Reporting Experience Data Model).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# [!UICONTROL Custom Metadata Details] Typ av rapportdata

[!UICONTROL Custom Metadata Details] Rapportering är en XDM-datatyp (Standard Experience Data Model) som definierar en struktur för lagring av anpassade metadata. The [!UICONTROL Custom Metadata Details] Rapporteringsdatatypen samlar in information som namn och värde på anpassade metadata som är associerade med innehåll eller interaktioner. Medierapporteringsfält används av Adobe-tjänster för att analysera de mediesamlingsfält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån.

![Ett diagram över datatypen Custom Metadata Details Reporting.](../images/data-types/the-custom-metadata-reporting.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Custom Metadata Field Name] | `name` | string | Namnet på det anpassade fältet. |
| [!UICONTROL Custom Metadata Field Value] | `value` | string | Värdet för det anpassade fältet. |

{style="table-layout:auto"}
