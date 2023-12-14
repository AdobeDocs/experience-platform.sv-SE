---
title: Datatyp för information om spelartillstånd
description: Läs mer om datatypen XDM (Player State Data Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# [!UICONTROL Player State Data Information] datatyp

[!UICONTROL Player State Data Information] är en XDM-datatyp (Standard Experience Data Model) som beskriver de olika lägena och deras förekomster i en mediespelare. Använd [!UICONTROL Player State Data Information] datatyp för inhämtning av olika spelarlägen, t.ex. helskärmsläge, stängd bildtext, bild-i-bild-läge och fokusläge. För varje läge registreras om läget är inställt, antalet förekomster och den totala varaktighet som det är aktivt under medieuppspelningen.

![Ett diagram över datatypen Player State Data.](../images/data-types/player-state-data-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Namnet på spelarläget. Uppräknade: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; med respektive innebörd. |
| [!UICONTROL Player State Set] | `isSet` | boolesk | Anger om spelarläget är inställt på det läget eller inte. |
| [!UICONTROL Player State Count] | `count` | heltal | Antalet gånger som det spelarläget har angetts för strömmen. |
| [!UICONTROL Player State Time] | `time` | heltal | Den totala längden för det spelarläget. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
