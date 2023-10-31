---
title: Aktivera målgrupper för kuraterade destinationer baserat på LiveRamp-identifierare
type: Tutorial
description: Lär dig hur du aktiverar målgrupper från Adobe Experience Platform till anslutna TV- och ljuddestinationer samt andra integreringar med LiveRamp RampID.
source-git-commit: adc7e66fa17484ccb9527650f197acc29ef4d0f1
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# Aktivera målgrupper för kuraterade destinationer baserat på LiveRamp-identifierare

Integrera Adobe Real-Time CDP med [!DNL LiveRamp] att aktivera målgrupper i en förvaltad lista över destinationer som använder [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) för aktivering, inklusive anslutna TV- och ljuddestinationer, t.ex. de som anges nedan.

>[!IMPORTANT]
>
>Du behöver inte importera eller på något sätt arbeta med LiveRamp-ID:n i Experience Platform-gränssnittet.
>
> Du kan exportera identiteter från Real-Time CDP, till exempel PII-baserade identifierare, kända identifierare och anpassade ID:n, enligt beskrivningen i [LiveRamp-dokumentation](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Dessa identiteter matchas sedan med [!DNL LiveRamp RampIDs] längre fram i processen.


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

Du kan aktivera målgrupper till anslutna TV- och ljuddestinationer genom att gå igenom en tvåstegsprocess och använda [LiveRamp - introduktion](../catalog/advertising/liveramp-onboarding.md) och [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md) mål, vilket visas i bilden nedan.

![Bild som visar arbetsflödet för aktivering av målgrupper från Real-Time CDP till kuraterade destinationer via LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png)

Först exporterar ni era målgrupper från Real-Time CDP till [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) mål, som CSV-filer.

När du har exporterat dina målgrupper kan du aktivera dem med [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) mål.

>[!TIP]
>
>Med den här processen kan ni aktivera era målgrupper för t.ex. [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)och mycket mer, direkt från Real-Time CDP UI, utan att du behöver logga in på [!DNL LiveRamp] aktiveringskonto.

### Steg 1: Skicka era målgrupper från Experience Platform till LiveRamp via [!DNL LiveRamp - Onboarding] mål {#onboarding}

Det första du måste göra för att kunna aktivera dina målgrupper till kuraterade destinationer baserade på LiveRamp-ramp-ID:n är att **exportera era målgrupper från Experience Platform till[!DNL LiveRamp]**.

Du gör detta med **[!DNL LiveRamp - Onboarding]** mål.

![Experience Platform-gränssnittsbild som visar LiveRamp - Destinationskort för introduktion](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Så här konfigurerar du [!DNL LiveRamp - Onboarding] destinera och exportera era målgrupper från Experience Platform, läsa [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) måldokumentation.

>[!IMPORTANT]
>
>Vid export av filer till [!DNL LiveRamp - Onboarding] mål, Platform genererar en CSV-fil för varje [princip-ID för sammanslagning](../../profile/merge-policies/overview.md). Se [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) måldokumentation som innehåller detaljerad information om hur du validerar dataexporten till LiveRamp.


När du har exporterat dina målgrupper till LiveRamp kan du fortsätta [steg 2](#distribution).

>[!TIP]
>
>Innan du går till [steg 2](#distribution), [validera](../catalog/advertising/liveramp-onboarding.md#exported-data) att era målgrupper har exporterats till LiveRamp. Läs dokumentationen om [övervaka måldataflöden](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) och läs om den specifika övervakningsinformationen för [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Steg 2: Aktivera den medföljande målgruppen för uppkopplade TV- och ljuddestinationer via [!DNL LiveRamp - Distribution] mål {#distribution}

Efter att du har [validerad](../catalog/advertising/liveramp-onboarding.md#exported-data) när era målgrupper har exporterats till LiveRamp är det dags att aktivera målgrupperna till de destinationer du föredrar, som [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), med mera.

Du aktiverar målgrupperna (exporterade i [steg 1](#onboarding)) genom att använda **[!DNL LiveRamp - Distribution]** mål.

![Experience Platform-gränssnittsbild som visar LiveRamp-distributionskortet](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Så här konfigurerar du **[!DNL LiveRamp - Distribution]** och aktivera de målgrupper som du har exporterat i [steg 1](#onboarding), läsa [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) måldokumentation.

>[!IMPORTANT]
>
>I **målgruppsval** steg i **[!DNL LiveRamp - Distribution]** mål måste du välja *exakt samma målgrupper* som du har exporterat till [LiveRamp - introduktion](../catalog/advertising/liveramp-onboarding.md) mål in [steg 1](#onboarding).

När du konfigurerar **[!DNL LiveRamp - Distribution]** måste du skapa en dedikerad anslutning för varje nedladdningsbart mål som du vill använda (Roku, Disney osv.).

>[!TIP]
>
>När du namnger målet rekommenderar Adobe följande format: `LiveRamp - Downstream Destination Name`. Det här namnmönstret hjälper dig att snabbt identifiera dina mål i [Bläddra](../ui/destinations-workspace.md#browse) -fliken i målarbetsytan.
><br>
>Exempel: `LiveRamp - Roku`.

![Skärmbild av användargränssnittet för plattformen med flera LiveRamp-mål.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Exporterade data/Validera dataexport {#exported-data}

Så här validerar du den lyckade exporten av era målgrupper till [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) mål, se dokumentationen om [övervaka måldataflöden](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) och läs om den specifika övervakningsinformationen för [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Om du vill validera att era målgrupper har aktiverats på valfri annonsplattform (som Roku, Disney med flera) loggar du in på målplattformskontot och kontrollerar aktiveringsvärdena.
