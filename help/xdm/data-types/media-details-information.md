---
title: Datatyp för medieinformation
description: Läs mer om datatypen XDM (Media Details Information Experience Data Model).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL Media details information] datatyp

[!UICONTROL Media details information] är en XDM-datatyp (Experience Data Model) som samlar viktig information om mediespelningshändelser. Använd [!UICONTROL Media details information] datatyp för att bland annat hämta information om exempelvis spelhuvudets position i innehållet, unika sessionsidentifierare och olika kapslade egenskaper för sessionen. Den här datatypen ger en omfattande översikt över uppspelningsupplevelsen, som gör det möjligt att spåra och analysera mediekonsumtionsmönster och associerade händelser under uppspelningssessioner.

+++Välj för att visa ett diagram över [!UICONTROL Media details information] datatyp.
![Ett diagram över [!UICONTROL Media details information] datatyp.](../images/data-types/media-details-information.png)
+++

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Playhead] | `playhead` | heltal | Spelhuvudet representerar den aktuella uppspelningspositionen i medieinnehållet. För direktsänt innehåll anger den aktuella sekunden på dagen (0 &lt;= spelhuvud &lt; 86400). För inspelat innehåll återspeglas den aktuella sekunden av innehållets längd (0 &lt;= playhead &lt; innehållslängd). |
| [!UICONTROL Media Session ID] | `sessionID` | string | Media Session ID identifierar en instans av en innehållsström under en enskild uppspelningssession. Det fungerar som en distinkt identifierare för att spåra och hantera den specifika uppspelningsupplevelsen som är kopplad till en användare eller ett visningsprogram. |
| [!UICONTROL Session Details] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Sessionsinformation omfattar omfattande information som är kopplad till upplevelsehändelsen och ger insikter om användarinteraktioner, varaktighet och sammanhangsberoende data som är relevanta för uppspelningssessionen. |
| [!UICONTROL Advertising Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Reklaminformationen avser specifik information om annonsaktiviteter under upplevelsehändelsen. Detta inkluderar annonsmetadata, målinriktningsinformation och resultatstatistik. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Information om reklamrutor innehåller information om annonstavlor i upplevelsehändelsen. Det ger insikter om annonssekvenser, innehåll och engagemangsmått. |
| [!UICONTROL Chapter Details] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Kapiteldetaljer samlar in data relaterade till kapitlen eller segmenterade delar av innehållet. Den innehåller information om kapitelmarkörer, tidslinjer och associerade metadata. |
| [!UICONTROL Error Details] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Felinformation innehåller information om fel som uppstod under upplevelsehändelsen. Detta inkluderar felkoder, beskrivningar, tidsstämplar och relevanta sammanhangsberoende data. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE (Quality of Experience) Information samlar in prestandarelaterade mått och användarupplevelsedata. Den ger insikter om kvalitet, lyhördhet och användarinteraktioner. |
| [!UICONTROL List Of States Start] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Lägen Start tillhandahåller en array som listar lägena i början av upplevelsehändelsen. Den innehåller data om uppspelning, användaråtgärder eller innehållsinformation. |
| [!UICONTROL List Of States End] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Lägesslut innehåller en array som listar lägena när upplevelsehändelsen avslutas. Den innehåller information om de slutliga uppspelningslägena eller innehållsstatusen. |
| [!UICONTROL List Of States] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Egenskapen states är en array som fångar olika lägen genom hela upplevelsehändelsen. Den här egenskapen innehåller sekventiella data om uppspelning, användaråtgärder eller innehållsändringar. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Anpassade metadata innehåller användardefinierade eller extra metadata som är associerade med upplevelsehändelsen. Med dessa metadata kan personaliserade eller specifika data inkluderas i händelsekontexten. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
