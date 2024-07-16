---
description: Använd kontrollpanelen [!UICONTROL Profile Enrichment] för att förstå om profilberikande jobb kördes och slutfördes samt för att visa grundläggande mått för att mäta effektiviteten av berikningarna.
solution: Experience Platform
title: Övervaka profilanrikningsjobb
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Övervaka profilberikande jobb i användargränssnittet {#monitor-profile-enrichment}

Använd kontrollpanelen [!UICONTROL Profile Enrichment] för att förstå om profilberikande jobb kördes och slutfördes samt för att visa grundläggande mått för att mäta effektiviteten av berikningarna.

I [Plattformsgränssnittet](https://platform.adobe.com) väljer du **[!UICONTROL Monitoring]** i den vänstra navigeringen för att komma åt [!UICONTROL Monitoring]-instrumentpanelen. I visningsväljaren väljer du **B2B-flöde** för att visa instrumentpanelselementen som är specifika för [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Kontrollpanelen [!UICONTROL Monitoring] innehåller grundläggande mått från den senaste lyckade körningen och jobbstatus upp till 90 dagar tidigare.

## Profilberikning för relaterade konton {#related-accounts}

Kontrollpanelen [!UICONTROL Related accounts] visar grundläggande mått och status för det dagliga jobbet som är specifikt för profilanrikningen [Relaterade konton](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Visuell indikation på hur du kommer till övervakningsskärmen för profilberikande jobb i användargränssnittet för Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Data på kortet **[!UICONTROL Metrics]** innehåller grundläggande mått från den senaste lyckade körningen av jobbet Relaterade konton.

Följande mått är tillgängliga för relaterade kontouppgifter:

| Mått | Beskrivning |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Anger det totala antalet kontoprofiler som din organisation har åtkomst till. |
| **[!UICONTROL Account groups]** | Anger antalet kontogrupper som har grupperats av det relaterade maskininlärningsjobbet för konton. |
| **[!UICONTROL Single-account groups]** | Anger antalet konton som inte är grupperade tillsammans med andra konton. |
| **[!UICONTROL Largest group size]** | Anger storleken på den största relaterade kontogruppen. Den högsta tillåtna gruppstorleken är 30. |
| **[!UICONTROL Median group size]** | Anger medianstorleken för relaterade kontogrupper i din organisation. |
| **[!UICONTROL Last successful run]** | Anger datum och tid för den senaste slutförda jobbkörningen för relaterade konton. |
| **[!UICONTROL Status]** | Anger status (slutförd, misslyckad eller bearbetad) för det relaterade kontojobbet. |
| **[!UICONTROL Message]** | Anger ett fel- eller varningsmeddelande för en viss jobbkörning. |

## Lead till kontomatchningsprofilens berikning {#lead-to-account-matching}

Kontrollpanelen [!UICONTROL Lead to account matching] visar grundläggande mått och daglig jobbkörningsstatus som är specifik för profilberikning för [lead till konto som matchar](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Lead till kontomatchningsprofilens berikning](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Följande mått är tillgängliga för lead-till-konto-matchande profilberikande jobb:

| Mått | Beskrivning |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Anger det totala antalet personer som är associerade med ett konto. |
| **[!UICONTROL Total accounts]** | Anger det totala antalet konton. |
| **[!UICONTROL Existing persons with accounts]** | Anger antalet personer som redan är associerade med ett konto från datakällorna. |
| **[!UICONTROL Persons matched]** | Anger antalet personer som matchades mot ett konto. |
| **[!UICONTROL Persons unmatched]** | Anger antalet personer som inte matchades mot ett konto. |
| **[!UICONTROL Last successful run]** | Anger datum och tid för den senaste lyckade lead-till-kontomatchningsjobbkörningen. |
| **[!UICONTROL Status]** | Anger status (slutförd, misslyckades eller bearbetad) för lead-till-kontomatchningsjobbet. |

## Profil för prediktiv analys av lead- och kontopoäng {#predictive-lead-to-account-scoring}

Kontrollpanelen [!UICONTROL Predictive lead and account scoring] visar grundläggande mått och daglig jobbkörningsstatus som är specifik för profilberikning för [Predictive lead and account scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) .

![Profil för prediktiv lead- och kontopoängsättning ](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Följande mätvärden är tillgängliga för prediktiva lead- och kontopoängsprofiler:

| Mått | Beskrivning |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Anger startdatum och starttid för körningen av det prediktiva lead- och kontobedömningsjobbet. |
| **[!UICONTROL Processing time]** | Den totala tid det tog för jobbet att slutföras. |
| **[!UICONTROL Score name]** | Jobbets poängnamn. |
| **[!UICONTROL Profile type]** | Typ av poäng: <ul><li>Person</li><li>Konto</li></ul>. |
| **[!UICONTROL Job type]** | Typ av jobb:<ul><li>Poäng</li><li>Utbildning</li>. |
| **[!UICONTROL Status]** | Anger status (slutförd, misslyckad eller bearbetning) för det prediktiva lead- och kontobedömningsjobbet. |

## Gränssnittskontroller {#ui-controls}

I det här avsnittet beskrivs olika gränssnittsalternativ (UI) i övervakningsgränssnittet, som gör att du kan filtrera mätvärdena som visas på sidan.

Använd pilikonen (![pilikon](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) för att expandera eller stänga kortet högst upp på skärmen, som visar översiktsinformation om profilberikningsjobb.

![Skärminspelning som visar gränssnittskontrollen för pilikonen.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Använd växlingsknappen **[!UICONTROL Metrics and graphs]** för att stänga vyn som visar de senaste måtten.

![Skärminspelning som visar växlingsknappen för mått och diagram.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Använd växlingsknappen **[!UICONTROL Show failures only]** om du bara vill visa misslyckade profilberikande jobb.

![Skärminspelning som visar växlingsknappen Visa endast fel.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen kan du nu övervaka och förstå mätvärden för profilanrikningsjobb. Mer information finns i följande dokument:

* [Relaterade konton i Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Fliken Relaterade konton i gränssnittsguiden för kontoprofiler](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead till kontomatchning i Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Prediktiv lead- och kontobedömning i Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
