---
title: Datatyp för information om mediainsamling
description: Läs mer om datatypen XDM (Media Collection Details Experience Data Model).
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# [!UICONTROL Media Collection Details] datatyp

[!UICONTROL Media Collection Details] är en XDM-datatyp (Experience Data Model) som samlar viktig information om mediespelningshändelser. Använd [!UICONTROL Media Collection Details] datatyp för att bland annat hämta information om exempelvis spelhuvudets position i innehållet, unika sessionsidentifierare och olika kapslade egenskaper för sessionen. Den här datatypen ger en omfattande översikt över uppspelningsupplevelsen som gör det möjligt att spåra och analysera mönster för mediekonsumtion och associerade händelser under uppspelningssessioner.

>[!NOTE]
>
>Media Collection-fält samlar in data och skickar dem till andra Adobe-tjänster för vidare bearbetning. Media Reporting-fält används av Adobe-tjänster för att analysera de Media Collection-fält som skickas av användarna. Dessa data, tillsammans med andra specifika användarvärden, beräknas och rapporteras utifrån.

+++Välj för att visa ett diagram över [!UICONTROL Media Collection details] datatyp.
![Ett diagram över [!UICONTROL Media Collection details information] datatyp.](../images/data-types/media-collection-details.png)
+++

| Visningsnamn | Egenskap | Händelser som krävs för | Datatyp | Beskrivning |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Advertising Details] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Samling](./advertising-details-collection.md) | Reklaminformationen avser specifik information om annonsaktiviteter under upplevelsehändelsen. Detta inkluderar annonsmetadata, målinriktningsinformation och resultatstatistik. |
| [!UICONTROL Advertising Pod Details] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Samling](./advertising-pod-details-collection.md) | Information om reklamrutor innehåller information om annonstavlor i upplevelsehändelsen. Det ger insikter om annonssekvenser, innehåll och engagemangsmått. |
| [!UICONTROL Chapter Details] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Samling](./chapter-details-collection.md) | Kapiteldetaljer samlar in data relaterade till kapitlen eller segmenterade delar av innehållet. Den innehåller information om kapitelmarkörer, tidslinjer och associerade metadata. |
| [!UICONTROL Error Details] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Samling](./error-details-collection.md) | Felinformation innehåller information om fel som uppstod under upplevelsehändelsen. Detta inkluderar felkoder, beskrivningar, tidsstämplar och relevanta sammanhangsberoende data. |
| [!UICONTROL List Of States End] | `statesEnd` | Används i `statesUpdate` | [[!UICONTROL statesEnd] - Samling](./list-of-states-end-collection.md) | Lägesslut innehåller en array som listar lägena när upplevelsehändelsen avslutas. Den innehåller information om de slutliga uppspelningslägena eller innehållsstatusen. |
| [!UICONTROL List Of States Start] | `statesStart` | Används i `statesUpdate` | [[!UICONTROL statesStart] - Samling](./list-of-states-start-collection.md) | Lägen Start tillhandahåller en array som listar lägena i början av upplevelsehändelsen. Den innehåller data om uppspelning, användaråtgärder eller innehållsinformation. |
| [!UICONTROL Qoe Data Details] | `qoeDataDetails` | Valfritt för alla | [[!UICONTROL qoeDataDetails] - Samling](./qoe-data-details-collection.md) | QoE (Quality of Experience) Information samlar in prestandarelaterade mått och användarupplevelsedata. Den ger insikter om kvalitet, lyhördhet och användarinteraktioner. |
| [!UICONTROL Session Details] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Samling](./session-details-collection.md) | Sessionsinformation omfattar omfattande information som är kopplad till upplevelsehändelsen och ger insikter om användarinteraktioner, varaktighet och sammanhangsberoende data som är relevanta för uppspelningssessionen. |
| [!UICONTROL The Custom Metadata] | `customMetadata` | Valfritt för `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Samling](./custom-metadata-details-collection.md) | Anpassade metadata innehåller användardefinierade eller extra metadata som är associerade med upplevelsehändelsen. Med dessa metadata kan personaliserade eller specifika data inkluderas i händelsekontexten. |
| [!UICONTROL Media Session ID] | `sessionID` | Alla händelser **utom** `sessionStart` och nedladdat innehåll. | string | Media Session ID identifierar en instans av en innehållsström under en enskild uppspelningssession. Det fungerar som en distinkt identifierare för att spåra och hantera den specifika uppspelningsupplevelsen som är kopplad till en användare eller ett visningsprogram.<br><em>Obs!<em>`sessionId` skickas för alla händelser utom `sessionStart` och för alla nedladdade händelser. |
| [!UICONTROL Playhead] | `playhead` | Alla händelser | heltal | Spelhuvudet representerar den aktuella uppspelningspositionen i medieinnehållet. För direktsänt innehåll anger den aktuella sekunden på dagen (0 &lt;= spelhuvud &lt; 86400). För inspelat innehåll återspeglas den aktuella sekunden av innehållets längd (0 &lt;= playhead &lt; innehållslängd). |

{style="table-layout:auto"}
