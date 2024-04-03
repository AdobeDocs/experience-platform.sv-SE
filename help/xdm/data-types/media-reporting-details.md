---
title: Datatypen Media Reporting Details
description: Läs mer om datatypen XDM (Media Reporting Details Experience Data Model).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!UICONTROL Media Reporting Details] datatyp

>[!NOTE]
>
>Media Collection-fält samlar in data och skickar dem till andra Adobe-tjänster för vidare bearbetning. Media Reporting-fält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån.

[!UICONTROL Media Reporting Details] är en XDM-datatyp (Experience Data Model) som samlar viktig information om mediespelningshändelser. Använd [!UICONTROL Media Reporting Details] datatyp för att bland annat hämta information om exempelvis spelhuvudets position i innehållet, unika sessionsidentifierare och olika kapslade egenskaper för sessionen. Den här datatypen ger en omfattande översikt över uppspelningsupplevelsen som gör det möjligt att spåra och analysera mönster för mediekonsumtion och associerade händelser under uppspelningssessioner.

>[!NOTE]
>
>De fält som anges nedan används inte direkt för att skapa begäranden. I stället sammanställs fältsamlingen som skickas till Adobe Experience Platform eller Adobe Analytics från dina data och mätvärden infogas eller bearbetas sedan av serverinfrastrukturen. Medan Platform samlar in olika typer av användarhändelser, fokuserar rapporterna på specifika händelser, som `media.sessionStart`, `media.adStart`och `media.sessionComplete`. Det innebär att även om du överför 12 typer av händelser under samlingen, kommer dina rapporter endast att innehålla uppdelningar baserade på de fem händelser som listas nedan.

+++Välj för att visa ett diagram över [!UICONTROL Media Reporting Details] datatyp.
![Ett diagram över [!UICONTROL Media Reporting Details] datatyp.](../images/data-types/media-reporting-details.png)
+++

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Reklaminformationen avser specifik information om annonsaktiviteter under upplevelsehändelsen. Detta inkluderar annonsmetadata, målinriktningsinformation och resultatstatistik. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Information om reklamrutor innehåller information om annonstavlor i upplevelsehändelsen. Det ger insikter om annonssekvenser, innehåll och engagemangsmått. |
| [!UICONTROL Chapter Details] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Kapiteldetaljer samlar in data relaterade till kapitlen eller segmenterade delar av innehållet. Den innehåller information om kapitelmarkörer, tidslinjer och associerade metadata. |
| [!UICONTROL List Of States] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | Egenskapen states är en array som fångar olika lägen genom hela upplevelsehändelsen. Den här egenskapen innehåller sekventiella data om uppspelning, användaråtgärder eller innehållsändringar. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE (Quality of Experience) Information samlar in prestandarelaterade mått och användarupplevelsedata. Den ger insikter om kvalitet, lyhördhet och användarinteraktioner. |
| [!UICONTROL Session Details] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Sessionsinformation omfattar omfattande information som är kopplad till upplevelsehändelsen och ger insikter om användarinteraktioner, varaktighet och sammanhangsberoende data som är relevanta för uppspelningssessionen. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Anpassade metadata innehåller användardefinierade eller extra metadata som är associerade med upplevelsehändelsen. Med dessa metadata kan personaliserade eller specifika data inkluderas i händelsekontexten. |
| [!UICONTROL Playhead] | `playhead` | heltal | Spelhuvudet representerar den aktuella uppspelningspositionen i medieinnehållet. För direktsänt innehåll anger den aktuella sekunden på dagen (0 &lt;= spelhuvud &lt; 86400). För inspelat innehåll återspeglas den aktuella sekunden av innehållets längd (0 &lt;= playhead &lt; innehållslängd). |

{style="table-layout:auto"}
