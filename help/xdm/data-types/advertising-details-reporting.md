---
title: Typ av rapportering av annonsinformation
description: Läs mer om datatypen Advertising Details Reporting Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# [!UICONTROL Advertising Details] Typ av rapportdata

[!UICONTROL Advertising Details] Rapportering är en XDM-datatyp (Standard Experience Data Model) som samlar in viktiga attribut relaterade till annonser. Det innehåller information som annons-ID, annons- och kampanj-ID:n, längd, position i en sekvens, information om spelaren som återger annonsen och så vidare. Ni kan använda den här datatypen för att spåra och analysera olika aspekter av annonsresultat och engagemang, och ge insikter om hur målgrupperna interagerar med och svarar på olika annonser.

+++Välj om du vill visa ett diagram över datatypen Advertising Details Reporting.
![Ett diagram över datatypen Advertising Details Reporting.](../images/data-types/advertising-details-information.png)
+++

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Ad Name] | `friendlyName` | string | Annonsens läsbara namn. I rapporter är&quot;annonsnamn&quot; klassificeringen och&quot;annonsnamn (variabel)&quot; eVarna. |
| [!UICONTROL Ad ID] | `name` | string | Annonsens ID. Valfri kombination av heltal och/eller bokstav. |
| [!UICONTROL Ad Length Or Duration] | `length` | heltal | Längden på videoannonsen i sekunder. |
| [!UICONTROL Ad In Pod Position (Ad Start)] | `podPosition` | heltal | Indexvärdet för annonsen inuti den överordnade annonsen startar, till exempel har den första annonsen indexvärdet 0 och den andra annonsen indexvärdet 1. |
| [!UICONTROL Ad Player Name] | `playerName` | string | Namnet på spelaren som ansvarar för att återge annonsen. |
| [!UICONTROL Ad Advertiser] | `advertiser` | string | Det företag eller varumärke vars produkt visas i annonsen. |
| [!UICONTROL Ad Campaign] | `campaignID` | string | ID för annonskampanjen. |
| [!UICONTROL Ad Creative ID] | `creativeID` | string | Annonspersonalens ID. |
| [!UICONTROL Ad Site ID] | `siteID` | string | ID för annonsplatsen. |
| [!UICONTROL Ad Creative URL] | `creativeURL` | string | Webbadressen till annonsskaparen. |
| [!UICONTROL Ad Placement ID] | `placementID` | string | Annonsens placerings-ID. |
| [!UICONTROL Ad Completed] | `isCompleted` | boolesk | Spårar om annonsen har slutförts. |
| [!UICONTROL Ad Started] | `isStarted` | boolesk | Spårar om annonsen har startats. |
| [!UICONTROL Ad Time Played] | `timePlayed` | heltal | Den totala tiden (i sekunder) som har ägnats åt att titta på annonsen (det vill säga antalet sekunder som har spelats upp). |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
