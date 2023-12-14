---
title: Kapitelinformation, datatyp
description: Lär dig mer om datatypen Kapitel Details Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# [!UICONTROL Chapter Details Information] datatyp

[!UICONTROL Chapter Details Information] är en XDM-datatyp (Standard Experience Data Model) som beskriver olika attribut som rör kapitel eller segment i medieinnehåll. Använd [!UICONTROL Chapter Details Information] datatyp för att samla in information som kapitelnamn, varaktighet, position, ID, uppspelningsstatus (start/slutförd) och hur lång tid som har ägnats åt varje kapitel.

![Ett diagram över datatypen Kapitelinformation.](../images/data-types/chapter-details-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Chapter Name] | `friendlyName` | string | Namnet på kapitlet och/eller segmentet. |
| [!UICONTROL Chapter Length Or Duration] | `length` | heltal | **Obligatoriskt** Kapitelns längd i sekunder. |
| [!UICONTROL Chapter Offset] | `offset` | heltal | **Obligatoriskt** Kapitelns förskjutning i innehållet (i sekunder) från början. |
| [!UICONTROL Chapter Position] | `index` | heltal | **Obligatoriskt** Placeringen (index, heltal) av kapitlet inuti innehållet. |
| [!UICONTROL Chapter ID] | `ID` | string | Kapitelets automatiskt genererade ID. |
| [!UICONTROL Chapter Started] | `isStarted` | boolesk | Anger om kapitlet har startats. |
| [!UICONTROL Chapter Completed] | `isCompleted` | boolesk | Anger om kapitlet har slutförts. |
| [!UICONTROL Chapter Time Played] | `timePlayed` | heltal | Den tid som har ägnats åt kapitlet, i sekunder. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
