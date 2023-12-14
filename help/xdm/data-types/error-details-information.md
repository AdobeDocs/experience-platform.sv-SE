---
title: Datatypen Felinformation
description: Läs mer om datatypen XDM (Error Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# [!UICONTROL Error Details Information] datatyp

[!UICONTROL Error Details Information] är en XDM-datatyp (Standard Experience Data Model) som beskriver felinformationen. Använd [!UICONTROL Error Details Information] datatyp för att samla in information om felkällan och identifieringen. Fel-ID:t identifierar felet och felkällan anger om det kommer från spelaren eller en extern källa.

![Ett diagram över datatypen Error Details.](../images/data-types/error-details-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Error ID] | `name` | string | Fel-ID. |
| [!UICONTROL Error Source] | `source` | string | Felkällan. Uppräknad: &quot;player&quot;, &quot;external&quot; med respektive innebörd. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
