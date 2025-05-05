---
title: Aktivera målgrupper för kuraterade destinationer baserat på LiveRamp-identifierare
type: Tutorial
description: Lär dig hur du aktiverar målgrupper från Adobe Experience Platform till anslutna TV- och ljuddestinationer samt andra integreringar med LiveRamp RampID.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Aktivera målgrupper för kuraterade destinationer baserat på LiveRamp-identifierare

Använd Adobe Real-Time CDP-integreringen med [!DNL LiveRamp] för att aktivera målgrupper till en förvaltad lista med mål som använder [[!DNL [LiveRamp RampID]]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) för aktivering, inklusive anslutna TV- och ljudmål, som de som listas nedan.

>[!IMPORTANT]
>
>Du behöver inte importera eller på något sätt arbeta med LiveRamp-ID:n i Experience Platform-gränssnittet.
>
> Du kan exportera identiteter från Real-Time CDP, till exempel PII-baserade identifierare, kända identifierare och anpassade ID:n, enligt beskrivningen i den officiella [LiveRamp-dokumentationen](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Dessa identiteter matchas sedan med [!DNL LiveRamp RampIDs] längre fram i aktiveringsprocessen.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgrupper från Real-Time CDP till de mål som anges ovan, direkt från Real-Time CDP användargränssnitt.

## Aktiveringsarbetsflöde {#workflow}

Du aktiverar målgrupper till anslutna TV- och ljuddestinationer genom att gå igenom en tvåstegsprocess och genom att använda [LiveRamp - OnBoarding](../catalog/advertising/liveramp-onboarding.md) och [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md) -destinationerna, vilket visas i bilden nedan.

![Bild som visar arbetsflödet för aktivering av målgrupper från Real-Time CDP till kuraterade mål via LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Först exporterar du dina målgrupper från Real-Time CDP till målet [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) som CSV-filer.

När du har exporterat dina målgrupper aktiverar du dem med hjälp av målet [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!TIP]
>
>Med den här processen kan du aktivera dina målgrupper till mål som [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) med flera, direkt från användargränssnittet i Real-Time CDP, utan att behöva logga in på ditt [!DNL LiveRamp]-konto för aktivering.

### Videosjälvstudiekurs {#video}

Titta på videon nedan för att få en komplett förklaring av arbetsflödet som beskrivs på den här sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Steg 1: Skicka dina målgrupper från Experience Platform till LiveRamp via målet [!DNL LiveRamp - Onboarding] {#onboarding}

Det första du måste göra för att aktivera dina målgrupper till kuraterade mål baserat på LiveRamp-ramp-ID:n är att **exportera dina målgrupper från Experience Platform till[!DNL LiveRamp]**.

Det gör du med målet **[!DNL LiveRamp - Onboarding]**.

![Experience Platform-gränssnittsbild som visar LiveRamp - Destinationskort för nyintroduktion](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Läs [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)-måldokumentationen om du vill lära dig hur du konfigurerar [!DNL LiveRamp - Onboarding]-målet och exporterar dina målgrupper från Experience Platform.

>[!IMPORTANT]
>
>När du exporterar filer till målet [!DNL LiveRamp - Onboarding] genererar Experience Platform en CSV-fil för varje [sammanfogningsprincip-ID](../../profile/merge-policies/overview.md) . Mer information om hur du validerar dataexporten till LiveRamp finns i [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)-måldokumentationen.


När du har exporterat dina målgrupper till LiveRamp fortsätter du till [steg 2](#distribution).

>[!TIP]
>
>Innan du går till [steg 2](#distribution) [validera](../catalog/advertising/liveramp-onboarding.md#exported-data) att dina målgrupper har exporterats till LiveRamp. Se dokumentationen om [övervakning av måldataflöden](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) och läs om den specifika övervakningsinformationen för [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Steg 2: Aktivera de inbyggda målgrupperna till anslutna TV- och ljuddestinationer via målet [!DNL LiveRamp - Distribution] {#distribution}

När du har [verifierat](../catalog/advertising/liveramp-onboarding.md#exported-data) att dina målgrupper har exporterats till LiveRamp är det dags att aktivera målgrupperna till önskade målplatser, till exempel [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney).

Du aktiverar målgrupperna (exporterade i [steg 1](#onboarding)) med hjälp av målet **[!DNL LiveRamp - Distribution]**.

![Experience Platform-gränssnittsbild som visar LiveRamp - distributionskortet](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Läs [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md)-måldokumentationen om du vill lära dig hur du konfigurerar **[!DNL LiveRamp - Distribution]**-målet och aktiverar de målgrupper som du har exporterat i [steg 1](#onboarding).

>[!IMPORTANT]
>
>I steget **målgruppsval** för målet **[!DNL LiveRamp - Distribution]** måste du välja *exakt samma målgrupper* som du har exporterat till målet [LiveRamp - onboarding](../catalog/advertising/liveramp-onboarding.md) i [steg 1](#onboarding).

När du konfigurerar **[!DNL LiveRamp - Distribution]**-målet måste du skapa en dedikerad anslutning för varje nedladdningsbart mål som du vill använda (Roku, Disney osv.).

>[!TIP]
>
>När du namnger målet rekommenderar Adobe följande format: `LiveRamp - Downstream Destination Name`. Det här namnmönstret hjälper dig att snabbt identifiera dina mål på fliken [Bläddra](../ui/destinations-workspace.md#browse) på arbetsytan för mål.
><br>
>Exempel: `LiveRamp - Roku`.

![Experience Platform UI-skärmbild med flera LiveRamp-mål.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Exporterade data/Validera dataexport {#exported-data}

Om du vill validera den lyckade exporten av dina målgrupper till [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md)-målet läser du dokumentationen om [övervakning av måldataflöden](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) och läser om den specifika övervakningsinformationen för [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Om du vill validera att era målgrupper har aktiverats på valfri annonsplattform (som Roku, Disney med flera) loggar du in på målplattformskontot och kontrollerar aktiveringsvärdena.
