---
description: Använd [!UICONTROL Profile Enrichment] Instrumentpanel för att förstå om profilberikningsjobben kördes och slutfördes samt för att visa grundläggande mått för att mäta effektiviteten av berikningarna.
solution: Experience Platform
title: Övervaka profilanrikningsjobb
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 842fe74b0b751c515a4faee437e1f94bd0662e11
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Övervaka profilberikande jobb i användargränssnittet {#monitor-profile-enrichment}

Använd [!UICONTROL Profile Enrichment] Instrumentpanel för att förstå om profilberikningsjobben kördes och slutfördes samt för att visa grundläggande mått för att mäta effektiviteten av berikningarna.

I [Plattformsgränssnitt](https://platform.adobe.com), markera **[!UICONTROL Monitoring]** från vänster navigering för att komma åt [!UICONTROL Monitoring] kontrollpanel. I vyväljaren väljer du **B2B-flöde** om du vill visa instrumentpanelselement som är specifika för [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  The [!UICONTROL Monitoring] Kontrollpanelen innehåller grundläggande mått från den senaste lyckade körningen och jobbstatus upp till 90 dagar tidigare.

## Profilberikning för relaterade konton {#related-accounts}

The [!UICONTROL Related accounts] på kontrollpanelen visas grundläggande mått och statusen för det dagliga jobbet som är specifikt för [Relaterade konton](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) profilberikning.

![Visuell indikation på hur du kommer till skärmen Profilanrikningsjobb i användargränssnittet i Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Data i **[!UICONTROL Metrics]** kortet innehåller grundläggande mått från den senaste lyckade körningen av jobbet Relaterade konton.

Följande mått är tillgängliga för relaterade kontouppgifter:

| Mått | Beskrivning |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Anger det totala antalet kontoprofiler som din organisation har åtkomst till. |
| **[!UICONTROL Account groups]** | Anger antalet kontogrupper som har grupperats av det relaterade maskininlärningsjobbet för konton. |
| **[!UICONTROL Single-account groups]** | Anger antalet konton som inte är grupperade tillsammans med andra konton. |
| **[!UICONTROL Largest group size]** | Anger storleken på den största relaterade kontogruppen. Den högsta tillåtna gruppstorleken är 30. |
| **[!UICONTROL Median group size]** | Anger medianstorleken för relaterade kontogrupper i din organisation. |
| **[!UICONTROL Last successful run]** | Anger datum och tid för den senaste slutförda jobbkörningen för relaterade konton. |
| **[!UICONTROL Status]** | Anger status (slutförd, misslyckades eller bearbetad) för det relaterade kontojobbet. |
| **[!UICONTROL Message]** | Anger ett fel- eller varningsmeddelande för en viss jobbkörning. |

## Lead till kontomatchningsprofilens berikning {#lead-to-account-matching}

The [!UICONTROL Lead to account matching] på kontrollpanelen visas grundläggande mått och daglig jobbkörningsstatus som är specifik för [Lead till kontomatchning](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) profilberikning.

![Lead till kontomatchningsprofilens berikning](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Följande mått är tillgängliga för lead-till-konto-matchande profilberikande jobb:

| Mått | Beskrivning |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Anger det totala antalet personer som är associerade med ett konto. |
| **[!UICONTROL Total accounts]** | Anger totalt antal konton. |
| **[!UICONTROL Existing persons with accounts]** | Anger antalet personer som redan är associerade med ett konto från datakällorna. |
| **[!UICONTROL Persons matched]** | Anger antalet personer som matchades mot ett konto. |
| **[!UICONTROL Persons unmatched]** | Anger antalet personer som inte matchades mot ett konto. |
| **[!UICONTROL Last successful run]** | Anger datum och tid för den senaste lyckade lead-till-kontomatchningsjobbkörningen. |
| **[!UICONTROL Status]** | Anger status (slutförd, misslyckades eller bearbetad) för lead-till-kontomatchningsjobbet. |

## Gränssnittskontroller {#ui-controls}

I det här avsnittet beskrivs olika gränssnittsalternativ (UI) i övervakningsgränssnittet, som gör att du kan filtrera mätvärdena som visas på sidan.

Använd pilikonen (![pilikon](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) om du vill expandera eller stänga av kortet högst upp på skärmen. Där visas i korthet information om profilberikande jobb.

![Skärminspelning som visar kontrollen för pilikonens användargränssnitt.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Använd **[!UICONTROL Metrics and graphs]** växla för att stänga vyn som visar de senaste mätvärdena.

![Skärminspelning som visar växlingsknappen för mått och diagram.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Använd **[!UICONTROL Show failures only]** växla endast för att visa misslyckade profilberikande jobb.

![Skärminspelning som visar växlingsknappen Visa endast fel.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen kan du nu övervaka och förstå mätvärden för profilanrikningsjobb. Mer information finns i följande dokument:

* [Relaterade konton i realtid CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Fliken Relaterade konton i gränssnittsguiden för kontoprofiler](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead till kontomatchning i realtid CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
