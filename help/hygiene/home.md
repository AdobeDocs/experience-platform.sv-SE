---
title: Översikt över avancerad hantering av datalivscykel
description: Med avancerad hantering av datalivscykel kan du hantera livscykeln för dina data genom att uppdatera eller rensa bort föråldrade eller felaktiga poster.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 1f82403d4f8f5639f6a9181a7ea98bd27af54904
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Advanced Data Lifecycle Management i Adobe Experience Platform

Adobe Experience Platform har en robust uppsättning verktyg för hantering av stora, komplicerade dataåtgärder för att samordna kundupplevelser. När data hämtas in till systemet över tid blir det allt viktigare att hantera dina datalager så att data används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationsprofiler anser det nödvändigt.

<!-- Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Dessa aktiviteter kan utföras med [[!UICONTROL Data Lifecycle] Arbetsyta i användargränssnittet](#ui) eller [API för datahygien](#api). När ett datatillverkarsjobb körs får systemet genomskinlighetsuppdateringar vid varje steg i processen. Se avsnittet om [tidslinjer och genomskinlighet](#timelines-and-transparency) om du vill ha mer information om hur varje jobbtyp visas i systemet.

>[!NOTE]
>
>Advanced Data Lifecycle Management stöder borttagning av datauppsättningar via [datauppsättningens förfalloslutpunkt](./api/dataset-expiration.md) och ID-borttagningar (radnivådata) med primära identiteter via [arbetsorderslutpunkt](./api/workorder.md). Du kan också hantera [förfallodatum för datauppsättning](./ui/dataset-expiration.md) och [postborttagningar](./ui/record-delete.md) via plattformsgränssnittet. Mer information finns i den länkade dokumentationen. Observera att datalifecycle inte stöder batchborttagning.

## [!UICONTROL Data Lifecycle] Arbetsyta för användargränssnitt {#ui}

Inställningen [!UICONTROL Data Lifecycle] -arbetsytan i plattformsgränssnittet gör att du kan konfigurera och schemalägga datalivscykelåtgärder, vilket hjälper dig att se till att dina poster bevaras som förväntat.

Detaljerade steg om hur du hanterar uppgifter i datalivscykeln i användargränssnittet finns i [användargränssnittshandbok för datalivscykel](./ui/overview.md).

## Data Hygiene API {#api}

Inställningen [!UICONTROL Data Lifecycle] Användargränssnittet byggs ovanpå Data Hygiene API, vars slutpunkter är tillgängliga så att du kan använda dem direkt om du föredrar att automatisera din datalivscykelaktivitet. Se [API-guide för datahygien](./api/overview.md) för mer information.

## Tidslinjer och genomskinlighet

[Ta bort post](./ui/record-delete.md) och förfrågningar om förfallodatum för datauppsättningar har sina egna tidslinjer för bearbetning och tillhandahåller genomskinlighetsuppdateringar vid viktiga punkter i sina respektive arbetsflöden.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Följande sker när en [förfallobegäran för datauppsättning](./ui/dataset-expiration.md) skapas:

| Stadie | Tid efter schemalagd förfallotid | Beskrivning |
| --- | --- | --- |
| Begäran har skickats | 0 timmar | En dataförvaltare eller integritetsanalytiker skickar en begäran om att en datauppsättning ska upphöra att gälla vid en viss tidpunkt. Förfrågan visas i [!UICONTROL Data Lifecycle UI] efter att den har skickats in och behåller statusen Väntande till den schemalagda förfallotiden, efter vilken begäran kommer att köras. |
| Datauppsättningen har släppts | 1 timme | Datauppsättningen tas bort från [lagersida för datauppsättning](../catalog/datasets/user-guide.md) i användargränssnittet. Data i datasjön tas bara bort på ett mjukt sätt, och kommer att finnas kvar tills processen är slut, varefter de kommer att tas bort. |
| Profilantalet har uppdaterats | 30 timmar | Beroende på innehållet i den datauppsättning som tas bort kan vissa profiler tas bort från systemet om alla deras komponentattribut är kopplade till den datauppsättningen. 30 timmar efter att datauppsättningen har tagits bort återspeglas eventuella förändringar i det totala antalet profiler i [widgetar för instrumentpanel](../dashboards/guides/profiles.md#profile-count-trend) och andra rapporter. |
| Målgrupper har uppdaterats | 48 timmar | När alla berörda profiler har uppdaterats är alla relaterade [målgrupper](../segmentation/home.md) uppdateras för att återspegla den nya storleken. Beroende på vilken datauppsättning som togs bort och vilka attribut du segmenterar på kan storleken på varje målgrupp öka eller minska som ett resultat av borttagningen. |
| Resor och destinationer uppdaterade | 50 timmar | [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [kampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)och [mål](../destinations/home.md) uppdateras enligt förändringar i relaterade segment. |
| Borttagningen har slutförts | 15 dagar | Alla data som rör datauppsättningen tas bort från datasjön. The [status för livscykeljobbet för data](./ui/browse.md#view-details) som tog bort datauppsättningen uppdateras för att återspegla detta. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Nästa steg

Det här dokumentet innehåller en översikt över funktionerna i Platform för datalivscykel. Om du vill komma igång med att göra datahygienbegäranden i användargränssnittet, se [Användargränssnittsguide](./ui/overview.md). Mer information om hur du skapar programmässigt jobb i Data Lifecycle finns i [API-guide för datahygien](./api/overview.md)
