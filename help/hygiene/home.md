---
title: Översikt över datahygien
description: Med Adobe Experience Platform Data Hygiene kan du hantera livscykeln för dina data genom att uppdatera eller rensa inaktuella eller felaktiga poster.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 0%

---

# Datahygien i Adobe Experience Platform

>[!IMPORTANT]
>
>Datahygien är för närvarande endast tillgänglig för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**.

Adobe Experience Platform har en robust uppsättning verktyg för hantering av stora, komplicerade dataåtgärder för att samordna kundupplevelser. När data hämtas in till systemet över tid blir det allt viktigare att hantera dina datalager så att data används som förväntat, uppdateras när felaktiga data behöver korrigeras och tas bort när organisationsprofiler anser det nödvändigt.

Plattformens datahygifunktioner gör att du kan hantera dina lagrade data genom följande:

* Schemalägga förfallodatum för automatiska datauppsättningar
* Ta bort enskilda poster från en eller alla datauppsättningar

>[!IMPORTANT]
>
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De är **not** som ska användas för förfrågningar om registrerade rättigheter (överensstämmelse) som rör sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). För all användning av regelefterlevnad [Adobe Experience Platform Privacy Service](../privacy-service/home.md) i stället.

Dessa aktiviteter kan utföras med [[!UICONTROL Data Hygiene] Arbetsyta i användargränssnittet](#ui) eller [API för datahygien](#api). När ett datahygijobb körs får systemet genomskinlighetsuppdateringar vid varje steg i processen. Se avsnittet om [tidslinjer och genomskinlighet](#timelines-and-transparency) om du vill ha mer information om hur varje jobbtyp visas i systemet.

## [!UICONTROL Data Hygiene] Arbetsyta i användargränssnittet {#ui}

The [!UICONTROL Data Hygiene] I plattformsgränssnittet kan du konfigurera och schemalägga dataåtgärder för hygienen, vilket gör att du kan vara säker på att dina poster bevaras som förväntat.

Detaljerade anvisningar om hur du hanterar datahygien i användargränssnittet finns i [Användargränssnittshandbok för datahygien](./ui/overview.md).

## API för datahygien {#api}

The [!UICONTROL Data Hygiene] Gränssnittet är byggt ovanpå API:t för datahygien, vars slutpunkter är tillgängliga för dig att använda direkt om du föredrar att automatisera din datahygien. Se [API-guide för datahygien](./api/overview.md) för mer information.

## Tidslinjer och genomskinlighet

Förfrågningar om radering och förfallodatum för datauppsättningar har sina egna bearbetningstidslinjer och tillhandahåller genomskinlighetsuppdateringar vid viktiga punkter i sina respektive arbetsflöden. Mer information om varje jobbtyp finns i avsnitten nedan.

### Utgångsdatum för datauppsättning {#dataset-expiration-transparency}

Följande sker när en [förfallobegäran för datauppsättning](./ui/dataset-expiration.md) skapas:

| Stadie | Tid efter schemalagd förfallotid | Beskrivning |
| --- | --- | --- |
| Begäran har skickats | 0 timmar | En datahanterare eller integritetsanalytiker skickar en begäran om att en datauppsättning ska upphöra att gälla vid en viss tidpunkt. Förfrågan visas i [!UICONTROL Data Hygiene UI] efter att den har skickats och har en väntande status fram till den schemalagda förfallotiden, efter vilken begäran kommer att köras. |
| Datauppsättningen tas bort | 1 timme | Datauppsättningen tas bort från [lagersida för datauppsättning](../catalog/datasets/user-guide.md) i användargränssnittet. Data i datasjön tas bara bort på ett mjukt sätt, och kommer att finnas kvar tills processen är slut, varefter de kommer att tas bort. |
| Profilantalet har uppdaterats | 30 timmar | Beroende på innehållet i den datauppsättning som tas bort kan vissa profiler tas bort från systemet om alla deras komponentattribut är kopplade till den datauppsättningen. 30 timmar efter att datauppsättningen har tagits bort återspeglas eventuella förändringar i det totala antalet profiler i [widgetar för instrumentpanel](../dashboards/guides/profiles.md#profile-count-trend) och andra rapporter. |
| Uppdaterade segment | 48 timmar | När alla profiler som påverkas har uppdaterats, är alla relaterade [segment](../segmentation/home.md) uppdateras för att återspegla deras nya storlek. Beroende på vilken datauppsättning som har tagits bort och vilka attribut du segmenterar på, kan storleken på varje segment öka eller minska till följd av borttagningen. |
| Uppdaterade resor och destinationer | 50 timmar | [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [kampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)och [mål](../destinations/home.md) uppdateras enligt förändringar i relaterade segment. |
| Hård borttagning slutförd | 14 dagar | Alla data som rör datauppsättningen tas bort från datasjön. The [hygienarbetsplatsens status](./ui/browse.md#view-details) som tog bort datauppsättningen uppdateras för att återspegla detta. |

{style=&quot;table-layout:auto&quot;}

### Posten tas bort {#record-delete-transparency}

>[!IMPORTANT]
>
>Borttagning av arkivhandlingar är endast tillgängligt för organisationer som har köpt Adobe Healthcare Shield.

Följande sker när en [postborttagningsbegäran](./ui/record-delete.md) skapas:

| Stadie | Tid efter att begäran har skickats | Beskrivning |
| --- | --- | --- |
| Begäran har skickats | 0 timmar | En datahanterare eller integritetsanalytiker skickar en begäran om radering av poster. Förfrågan visas i [!UICONTROL Data Hygiene UI] efter det att den har skickats in. |
| Profilsökningar har uppdaterats | 3 timmar | Ändringen av antalet profiler som orsakas av den borttagna identiteten återspeglas i [widgetar för instrumentpanel](../dashboards/guides/profiles.md#profile-count-trend) och andra rapporter. |
| Uppdaterade segment | 24 timmar | När profilerna har tagits bort är alla relaterade [segment](../segmentation/home.md) uppdateras för att återspegla deras nya storlek. |
| Uppdaterade resor och destinationer | 26 timmar | [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [kampanjer](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)och [mål](../destinations/home.md) uppdateras enligt förändringar i relaterade segment. |
| Poster som är mjuka och har tagits bort i datasjön | 7 dagar | Data tas bort på ett mjukt sätt från datasjön. |
| Datautvinning slutförd | 14 dagar | The [hygienarbetsplatsens status](./ui/browse.md#view-details) Uppdateringar som anger att jobbet har slutförts, vilket innebär att datautbyte har slutförts på sjön och att de relevanta posterna har tagits bort. |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

I det här dokumentet finns en översikt över plattformens datahygien. Information om hur du kommer igång med att göra förfrågningar om datahygien i användargränssnittet finns i [Användargränssnittsguide](./ui/overview.md). Om du vill veta hur du skapar datahygien-jobb programmatiskt kan du läsa [API-guide för datahygien](./api/overview.md)
