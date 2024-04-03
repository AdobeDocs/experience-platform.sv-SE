---
title: Advertising Pod Details Reporting, datatyp
description: Läs mer om datatypen Advertising Pod Details Reporting Experience Data Model (XDM).
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# [!UICONTROL Advertising Pod Details Reporting] datatyp

[!UICONTROL Advertising Pod Details Reporting] är en XDM-datatyp (Standard Experience Data Model). Den definierar en sekvens eller en grupp annonser som vanligtvis spelas upp i följd under innehållsbrytningar. Använd [!UICONTROL Advertising Pod Details Reporting] datatyp för att samla in information som annonsbrytnings-ID, ett eget namn för annonsbrytningen, indexet för annonserna inom brytningen och förskjutningen för annonsbrytningen inom innehållets tidslinje på några sekunder.

![Ett diagram över datatypen Advertising Pod Details Reporting.](../images/data-types/advertising-pod-details-information.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | string | ID för annonsbrytningen. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | string | Det lättbegripliga namnet på annonsbrytningen. |
| [!UICONTROL Ad In Pod Position] | `index` | heltal | Indexvärdet för annonsen inuti den överordnade annonsradbrytningen. |
| [!UICONTROL Pod Offset] | `offset` | heltal | **Obligatoriskt** Annonsens förskjutning i innehållet, i sekunder. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
