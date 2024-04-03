---
title: Advertising Pod Details Collection datatyp
description: Läs mer om datatypen Advertising Pod Details Collection Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 2%

---

# [!UICONTROL Advertising Pod Details] Samlingsdatatyp

[!UICONTROL Advertising Pod Details] Samlingen är en XDM-datatyp (Standard Experience Data Model). Den definierar en sekvens eller en grupp annonser som vanligtvis spelas upp i följd under innehållsbrytningar. Använd [!UICONTROL Advertising Pod Details] Samlingsdatatyp för att samla in information som annonsbrytnings-ID, ett eget namn för annonsbrytningen, indexet för annonserna inom brytningen och förskjutningen för annonsbrytningen inom innehållets tidslinje på några sekunder.

![Ett diagram över datatypen Advertising Pod Details Collection.](../images/data-types/advertising-pod-details-collection.png)

| Visningsnamn | Egenskap | Datatyp | Obligatoriskt | Beskrivning |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| [!UICONTROL Ad In Pod Position] | `index` | heltal | Ja | Indexvärdet för annonsen inuti den överordnade annonsradbrytningen. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Nej | Det lättbegripliga namnet på annonsbrytningen. |
| [!UICONTROL Pod Offset] | `offset` | heltal | Ja | Annonsens förskjutning i innehållet, i sekunder. |
