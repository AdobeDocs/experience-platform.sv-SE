---
title: Datatyp för rapportering av spelarlägesdata
description: Läs mer om datatypen XDM (Player State Data Reporting Experience Data Model).
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Datatypen [!UICONTROL Player State Data Reporting]

[!UICONTROL Player State Data Reporting] är en XDM-datatyp (Standard Experience Data Model) som beskriver de olika lägena och deras förekomster i en mediespelare. Använd datatypen [!UICONTROL Player State Data Reporting] om du vill hämta olika spelarlägen, till exempel helskärm, stängd bildtext, bild-i-bild- och fokuslägen. För varje läge registreras om läget är inställt, antalet förekomster och den totala varaktighet som det är aktivt under medieuppspelningen.

![Ett diagram över datatypen Player State Data Reporting.](../images/data-types/player-state-data-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Player State Name] | `name` | string | Namnet på spelarläget. Uppräknade: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; med respektive innebörd. |
| [!UICONTROL Player State Set] | `isSet` | boolesk | Anger om spelarläget är inställt på det läget eller inte. |
| [!UICONTROL Player State Count] | `count` | heltal | Antalet gånger som det spelarläget har angetts för strömmen. |
| [!UICONTROL Player State Time] | `time` | heltal | Den totala längden för det spelarläget. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
