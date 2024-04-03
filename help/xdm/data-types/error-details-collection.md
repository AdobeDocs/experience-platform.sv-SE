---
title: Datatyp för insamling av felinformation
description: Läs mer om datatypen XDM (Error Details Collection Experience Data Model).
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# [!UICONTROL Error Details] Samlingsdatatyp

[!UICONTROL Error Details] Samlingen är en XDM-datatyp (Standard Experience Data Model) som beskriver felinformationen. Använd [!UICONTROL Error Details] Samlingsdatatyp för att samla in information om felkällan och identifiering. Fel-ID:t identifierar felet och felkällan anger om det kommer från spelaren eller en extern källa.

![Ett diagram över datatypen Error Details.](../images/data-types/error-details-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Nej | Fel-ID. |
| [!UICONTROL Error Source] | `source` | string | Nej | Felkällan. Uppräknad: &quot;player&quot;, &quot;external&quot; med respektive innebörd. |

{style="table-layout:auto"}
