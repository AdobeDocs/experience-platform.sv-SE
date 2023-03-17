---
title: Översikt över datahygien
description: Med Adobe Experience Platform Data Hygiene kan du hantera livscykeln för dina data genom att uppdatera eller rensa inaktuella eller felaktiga poster.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 2913e9e687843e566db4ebf2031e610d1891d4c9
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Datahygien i Adobe Experience Platform

>[!IMPORTANT]
>
>Datahygien är för närvarande endast tillgänglig för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**. De här funktionerna kommer att lanseras inom en snar framtid. Om du vill ha mer information om hur de kommer att bli tillgängliga kontaktar du Adobes servicerepresentant. Du kan dock göra det omedelbart [ta bort datauppsättningar via [!UICONTROL Datasets] UI](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform har en robust uppsättning verktyg för hantering av stora, komplicerade dataåtgärder för att samordna kundupplevelser. När data hämtas in till systemet över tid blir det allt viktigare att hantera dina datalager så att data används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationsprofiler anser det nödvändigt.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Dessa aktiviteter kan utföras med [[!UICONTROL Data Hygiene] Arbetsyta i användargränssnittet](#ui) eller [API för datahygien](#api). När ett datahygijobb körs får systemet genomskinlighetsuppdateringar vid varje steg i processen. Se avsnittet om [tidslinjer och genomskinlighet](#timelines-and-transparency) om du vill ha mer information om hur varje jobbtyp visas i systemet.

## [!UICONTROL Data Hygiene] Arbetsyta i användargränssnittet {#ui}

The [!UICONTROL Data Hygiene] I plattformsgränssnittet kan du konfigurera och schemalägga dataåtgärder för hygienen, vilket gör att du kan vara säker på att dina poster bevaras som förväntat.

Detaljerade anvisningar om hur du hanterar datahygien i användargränssnittet finns i [Användargränssnittshandbok för datahygien](./ui/overview.md).

## API för datahygien {#api}

The [!UICONTROL Data Hygiene] Gränssnittet är byggt ovanpå API:t för datahygien, vars slutpunkter är tillgängliga för dig att använda direkt om du föredrar att automatisera din datahygien. Se [API-guide för datahygien](./api/overview.md) för mer information.

## Tidslinjer och genomskinlighet

Förfrågningar om radering och förfallodatum för datauppsättningar har sina egna bearbetningstidslinjer och tillhandahåller genomskinlighetsuppdateringar vid viktiga punkter i sina respektive arbetsflöden.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Följande sker när en [förfallobegäran för datauppsättning](./ui/dataset-expiration.md) skapas:

| Stadie | Tid efter schemalagd förfallotid | Beskrivning |
| --- | --- | --- |
| Begäran har skickats | 0 timmar | En datahanterare eller integritetsanalytiker skickar en begäran om att en datauppsättning ska upphöra att gälla vid en viss tidpunkt. Förfrågan visas i [!UICONTROL Data Hygiene UI] efter att den har skickats och har en väntande status fram till den schemalagda förfallotiden, efter vilken begäran kommer att köras. |
| Datauppsättningen tas bort | 1 timme | Datauppsättningen tas bort från [lagersida för datauppsättning](../catalog/datasets/user-guide.md) i användargränssnittet. Data i datasjön tas bara bort på ett mjukt sätt, och kommer att finnas kvar tills processen är slut, varefter de kommer att tas bort. |
| Profilantalet har uppdaterats | 30 timmar | Beroende på innehållet i den datauppsättning som tas bort kan vissa profiler tas bort från systemet om alla deras komponentattribut är kopplade till den datauppsättningen. 30 timmar efter att datauppsättningen har tagits bort återspeglas eventuella förändringar i det totala antalet profiler i [widgetar för instrumentpanel](../dashboards/guides/profiles.md#profile-count-trend) och andra rapporter. |
| Uppdaterade segment | 48 timmar | När alla profiler som påverkas har uppdaterats, är alla relaterade [segment](../segmentation/home.md) uppdateras för att återspegla deras nya storlek. Beroende på vilken datauppsättning som har tagits bort och vilka attribut du segmenterar på, kan storleken på varje segment öka eller minska till följd av borttagningen. |
| Uppdaterade resor och destinationer | 50 timmar | [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [kampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)och [mål](../destinations/home.md) uppdateras enligt förändringar i relaterade segment. |
| Hård borttagning slutförd | 14 dagar | Alla data som rör datauppsättningen tas bort från datasjön. The [hygienarbetsplatsens status](./ui/browse.md#view-details) som tog bort datauppsättningen uppdateras för att återspegla detta. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Nästa steg

I det här dokumentet finns en översikt över plattformens datahygien. Information om hur du kommer igång med att göra förfrågningar om datahygien i användargränssnittet finns i [Användargränssnittsguide](./ui/overview.md). Om du vill veta hur du skapar datahygien-jobb programmatiskt kan du läsa [API-guide för datahygien](./api/overview.md)
