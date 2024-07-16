---
title: Advertising Pod Details Reporting, datatyp
description: Läs mer om datatypen Advertising Pod Details Reporting Experience Data Model (XDM).
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Datatypen [!UICONTROL Advertising Pod Details Reporting]

[!UICONTROL Advertising Pod Details Reporting] är en XDM-datatyp (Standard Experience Data Model). Den definierar en sekvens eller en grupp annonser som vanligtvis spelas upp i följd under innehållsbrytningar. Använd datatypen [!UICONTROL Advertising Pod Details Reporting] för att hämta information som annonsbrytnings-ID, ett eget namn för annonsbrytningen, indexet för annonserna inom brytningen och förskjutningen för annonsbrytningen inom innehållets tidslinje på några sekunder.

![Ett diagram över datatypen Advertising Pod Details Reporting.](../images/data-types/advertising-pod-details-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | string | ID för annonsbrytningen. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Det lättbegripliga namnet på annonsbrytningen. |
| [!UICONTROL Ad In Pod Position] | `index` | heltal | Indexvärdet för annonsen inuti den överordnade annonsradbrytningen. |
| [!UICONTROL Pod Offset] | `offset` | heltal | **Obligatoriskt** Annonsbrytningens förskjutning inuti innehållet, i sekunder. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
