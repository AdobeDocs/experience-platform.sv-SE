---
title: Datatyp för insamling av felinformation
description: Läs mer om datatypen XDM (Error Details Collection Experience Data Model).
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# [!UICONTROL Error Details] Samlingsdatatyp

[!UICONTROL Error Details]-samlingen är en XDM-datatyp (Standard Experience Data Model) som beskriver felinformationen. Använd datatypen [!UICONTROL Error Details] Samling för att samla in information om felkällan och identifieringen. Fel-ID:t identifierar felet och felkällan anger om det kommer från spelaren eller en extern källa.

![Ett diagram över datatypen Error Details.](../images/data-types/error-details-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Nej | Fel-ID. |
| [!UICONTROL Error Source] | `source` | string | Nej | Felkällan. Uppräknad: &quot;player&quot;, &quot;external&quot; med respektive innebörd. |

{style="table-layout:auto"}
