---
title: Översikt över livscykelhantering av avancerade data
description: Med Advanced Data Lifecycle Management kan ni hantera livscykeln för era data genom att uppdatera eller tömma inaktuella eller felaktiga poster.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a1502e8f1515ff73840b2926f5be355032dd4bab
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Avancerad livscykelhantering av data i Adobe Experience Platform

Adobe Experience Platform har en robust uppsättning verktyg för hantering av stora, komplicerade dataåtgärder för att samordna kundupplevelser. När data hämtas in till systemet över tid blir det allt viktigare att hantera dina datalager så att data används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationsprofiler anser det nödvändigt.

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Dessa aktiviteter kan utföras med arbetsytan [[!UICONTROL Data Lifecycle] i användargränssnittet &#x200B;](#ui) eller [API:t för datahygien](#api). När ett datatillverkarsjobb körs får systemet genomskinlighetsuppdateringar vid varje steg i processen. Mer information om hur varje jobbtyp visas i systemet finns i avsnittet [tidslinjer och genomskinlighet](#timelines-and-transparency).

>[!NOTE]
>
>Avancerad livscykelhantering för data stöder borttagning av datauppsättningar via [datamängdens slutpunkt](./api/dataset-expiration.md) och ID-borttagningar (radnivådata) med hjälp av primära identiteter via [arbetsorderslutpunkten](./api/workorder.md). Du kan också hantera [förfallodatum för datauppsättningar](./ui/dataset-expiration.md) och [borttagningar av poster](./ui/record-delete.md) via Experience Platform-gränssnittet. Mer information finns i den länkade dokumentationen. Observera att datalifecycle inte stöder batchborttagning.

## Arbetsytan i gränssnittet för [!UICONTROL Data Lifecycle] {#ui}

Med arbetsytan [!UICONTROL Data Lifecycle] i Experience Platform UI kan du konfigurera och schemalägga datalivscykelåtgärder, vilket säkerställer att dina poster bevaras som förväntat.

Detaljerade anvisningar om hur du hanterar livscykelaktiviteter för data i användargränssnittet finns i [användargränssnittshandboken för datatillgångar](./ui/overview.md).

## API för datahygien {#api}

Gränssnittet [!UICONTROL Data Lifecycle] är byggt ovanpå API:t för datahygien, vars slutpunkter är tillgängliga för dig att använda direkt om du föredrar att automatisera dina datalivscykelaktiviteter. Mer information finns i [API-handboken för datahygien](./api/overview.md).

## Tidslinjer och genomskinlighet {#timelines-and-transparency}

[Förfrågningar om borttagning av poster](./ui/record-delete.md) och förfallodatum för datauppsättningar har sina egna bearbetningstidslinjer och tillhandahåller genomskinlighetsuppdateringar vid viktiga punkter i sina respektive arbetsflöden.

>[!TIP]
>
>Om du vill övervaka din nuvarande användning mot kvotbegränsningar läser du [referensguiden för kvoter](./api/quota.md).\
>Information om berättiganderegler, månadstak, SLA-tidslinjer och undantagshanteringsprinciper finns i dokumentationen om [borttagning av post (UI)](./ui/record-delete.md#quotas) och [arbetsorder (API)](./api/workorder.md#quotas).

Följande inträffar när en [förfallobegäran](./ui/dataset-expiration.md) för en datauppsättning skapas:

| Stadie | Tid efter schemalagd förfallotid | Beskrivning |
| --- | --- | --- |
| Begäran har skickats | 0 timmar | En datahanterare eller integritetsanalytiker skickar en begäran om att en datauppsättning ska upphöra att gälla vid en viss tidpunkt. Begäran är synlig i [!UICONTROL Data Lifecycle UI] efter att den har skickats och har en väntande status fram till den schemalagda förfallotiden, efter vilken begäran kommer att köras. |
| Datauppsättningen tas bort från datasjön | 1 timme | Datauppsättningen tas bort från [datauppsättningens lagersida](../catalog/datasets/user-guide.md) i användargränssnittet. Data i datasjön tas bara bort på ett mjukt sätt, och kommer att finnas kvar tills processen är slut, varefter de kommer att tas bort. |
| Datauppsättningen tas bort från profiltjänsten | 3 timmar | Från och med nu kommer åtgärder som batchsegmentering och direktuppspelningssegmentering, förhandsgranskning eller uppskattning, export och åtkomst till enheter inte längre att läsa data från den här datauppsättningen. Informationen i profiltjänsten är endast mjuk och tas bort tills processen är klar. Därefter tas den bort. |
| Profilantal och målgrupper har uppdaterats | 48 timmar | När alla profiler som påverkas har uppdaterats uppdateras alla relaterade [målgrupper](../segmentation/home.md) så att deras nya storlek återspeglas. Beroende på vilken datauppsättning som har tagits bort och vilka attribut du segmenterar på, kan storleken på varje målgrupp öka eller minska på grund av borttagningen. Vid den här tidpunkten återspeglas eventuella ändringar i det totala antalet profiler i [instrumentpanelswidgetar](../dashboards/guides/profiles.md#profile-count-trend) och andra rapporter. |
| Uppdaterade resor och destinationer | 50 timmar | [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [kampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html) och [mål](../destinations/home.md) uppdateras enligt ändringar i relaterade segment. |
| Borttagningen har slutförts | 15 dagar | Alla data som är relaterade till datauppsättningen tas bort från datasjön och profiltjänsten. Status [för datatilleriet &#x200B;](./ui/browse.md#view-details) som tog bort datauppsättningen uppdateras för att återspegla detta. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Borttagningar av datauppsättningar i Amazon Web Services (AWS) kan fördröjas med ungefär tre timmar innan ändringarna tillämpas helt. Detta inkluderar upp till två timmar innan datauppsättningen flaggas för borttagning, följt av ytterligare en timme innan den tas bort helt från systemet. Borttagningsbegäranden för Experience Platform-instanser som använder Azure Data Lake resulterar däremot i omedelbara ändringar i alla affärsfunktioner.
>
>För AWS-användare kan fördröjningen påverka gruppsegmentering, direktuppspelningssegmentering, förhandsvisningar, uppskattningar, export och dataåtkomst. Denna fördröjning påverkar bara kunder som använder AWS eftersom Azure Data Lake-användare får omedelbara uppdateringar. För AWS-användare kan det ta upp till tre timmar för raderingsbegäranden att sprida sig fullt ut via alla system som påverkas. Justera dina förväntningar därefter.


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

I det här dokumentet finns en översikt över Experience Platform funktioner för datalivscykel. Om du vill komma igång med att göra datahygienbegäranden i användargränssnittet kan du läsa [användargränssnittshandboken](./ui/overview.md). Mer information om hur du skapar datalifecycle-jobb programmatiskt finns i [API-handboken för datahygien](./api/overview.md)
