---
title: Datatypen Advertising Details Reporting
description: Läs mer om datatypen Advertising Details Reporting Experience Data Model (XDM).
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Datatypen [!UICONTROL Advertising Details] för rapportering

[!UICONTROL Advertising Details]-rapportering är en XDM-datatyp (Standard Experience Data Model) som samlar in nyckelattribut relaterade till annonser. Det innehåller information som annons-ID, annons- och kampanj-ID:n, längd, position i en sekvens, information om spelaren som återger annonsen och så vidare. Ni kan använda den här datatypen för att spåra och analysera olika aspekter av annonsresultat och engagemang, och ge insikter om hur målgrupperna interagerar med och svarar på olika annonser.

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

Mer information om fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
