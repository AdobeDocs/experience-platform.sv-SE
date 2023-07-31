---
title: AI-widgetar för kunder i instrumentpanelen
description: Lär dig hur kundens AI ger viktiga insikter om förändring eller benägenhet för er organisations målgrupper i kundprofiler i realtid.
hide: true
hidefromtoc: true
source-git-commit: 74dcb35b389a962a5238c1fd5ef1370a76bdd57e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---

# Auditions dashboard - kundens AI-widgetar {#customer-ai-audiences-widgets}

Kund-AI används för att generera anpassade benägenhetspoäng som omsättning och konvertering för enskilda profiler i stor skala. Kunden gör detta genom att analysera befintliga data om kundupplevelsehändelser för att förutsäga **poängtal för bortfall eller konverteringsbenägenhet**. Dessa högkvalitativa kundbenägenhetsmodeller möjliggör mer exakt segmentering och målinriktning. The [fördelning av poäng](#customer-ai-distribution-of-scores) och [poängsammanfattning](#customer-ai-scoring-summary) insikter visar hur er målgrupp skiljer sig från mängden. Panelerna sätter fokus på vilka profiler som är de höga/låga/medelstora och hur de fördelas över dina profilantal.

<!-- 
THe links when required
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Customer AI distribution of scores] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_distributionOfScores"
>title="Fördelning av poäng"
>abstract="Den här widgeten visar fördelningen av det totala antalet profiler utifrån deras benägenhetspoäng i steg om fem procent. Distributionen av profilantalet bestäms av AI-modellen och den valda sammanfogningsprincipen. Du kan ändra AI-modellen i listrutan under widgettiteln."

The [!UICONTROL Customer AI distribution of scores] widgeten kategoriserar det totala antalet profiler utifrån deras benägenhetspoäng. Fördelningen av profilantalet bestäms av AI-modellen och den valda sammanfogningspolicyn och visualiseras sedan i steg om fem procent som anger deras benägenhet. Antalet profiler anges längs Y-axeln och benägenhetspoängen anges längs X-axeln.

>[!NOTE]
>
>Om visualiseringen är en konverteringsbenägenhetspoäng visas de höga poängen i grönt och de låga poängen i rött. Om du förutser kurvbenägenheten att detta vänds är de höga poängen röda och de låga poängen gröna. Mediefiltret förblir gult oavsett vilken typ av benägenhet du väljer.

Den AI-modell som avgör graden av benägenhet väljs i listruteväljaren under widgetens titel. Listrutan innehåller en lista över alla konfigurerade AI-modeller för kunder. Välj lämplig AI-modell för analysen i listan över tillgängliga modeller. Om det inte finns någon AI-modell för kunden instruerar ett meddelande i widgeten dig att konfigurera minst en AI-modell för kunden och tillhandahåller en hyperlänk till konfigurationssidan för kundens AI-modell. I dokumentationen finns instruktioner om [konfigurera en kundens AI-instans](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Välj listrutan direkt under fliken Översikt om du vill ändra den sammanfogningsprincip som avgör vilka profiler som tas med i analysen. Se avsnittet om [sammanfogningsprinciper](#merge-policies) för en kort beskrivning eller [översikt över sammanfogningsprincip](../../profile/merge-policies/overview.md) för mer information.

Om du vill navigera till sidan med detaljerade insikter för den valda kundens AI-modell väljer du **[!UICONTROL View model details]**.

![Kontrollpanelen Experience Platform Publiker med [!UICONTROL Customer AI distribution of scores] widget och [!UICONTROL View model details] markerad.](../images/segments/customer-ai-distribution-of-scores.png)

Sidan med detaljerad modellinformation visas.

![Sidan med insikter för kundens AI.](../images/profiles/customer-ai-insights-page.png)

Mer information om kundens AI finns på [gränssnittsguide för upptäckt av insikter](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Customer AI scoring summary] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_scoringSummary"
>title="Sammanfattning av poäng"
>abstract="Den här widgeten visar det totala antalet poängsatta profiler och kategoriserar dem i grupper som innehåller hög, medelhög och låg benägenhet. Nutdiagrammet visar den proportionella sammansättningen av de totala profilerna över hög, medel och låg benägenhet."

Den här widgeten visar det totala antalet profiler som har poängterats och kategoriserar dem i grupper som innehåller hög, medelhög och låg benägenhet som grön, gul respektive röd. Ett mundiagram används för att illustrera den proportionella kompositionen av de totala profilerna mellan hög-, medel- och låg-egenskaper som grönt, gult respektive rött. En profil ger hög benägenhet vid över 75, medelhög intensitet mellan 25 och 74 och låg benägenhet under 24. En teckenförklaring anger färgkoden och egenskapernas tröskelvärden. Profilantal för de höga, medelstora och låga egenskaperna visas i en dialogruta när markören hålls över respektive avsnitt i mundiagrammet.

>[!NOTE]
>
>Om visualiseringen är en konverteringsbenägenhetspoäng visas de höga poängen i grönt och de låga poängen i rött. Om du förutser kurvbenägenheten att detta vänds är de höga poängen röda och de låga poängen gröna. Mediefiltret förblir gult oavsett vilken typ av benägenhet du väljer.

I listrutan under widgetens rubrik finns en lista med alla konfigurerade AI-modeller för kunder. Välj lämplig AI-modell för analysen i listan över tillgängliga modeller. Om det inte finns någon AI-modell för kunden instruerar ett meddelande i widgeten dig att konfigurera minst en AI-modell för kunden och tillhandahåller en hyperlänk till konfigurationssidan för kundens AI-modell. Läs dokumentationen om [konfigurera en kundens AI-instans](../../intelligent-services/customer-ai/user-guide/configure.md) för detaljerade anvisningar.

>[!NOTE]
>
>Det totala antalet beräknade profiler beror på den valda sammanfogningsprincipen. Om du vill ändra den sammanfogningsprincip som används väljer du listrutan direkt under fliken Översikt. Se avsnittet om [sammanfogningsprinciper](#merge-policies) för en kort beskrivning eller [översikt över sammanfogningsprincip](../../profile/merge-policies/overview.md) för mer information.

![Kontrollpanelen Experience Platform Publiker med widgeten för sammanfattning av kundens AI-poäng markerad.](../images/segments/customer-ai-scoring-summary.png)

Välj **[!UICONTROL View model details]** för att navigera till sidan med detaljerade insikter för den valda kundens AI-modell. Mer information om kundens AI finns på [gränssnittsguide för upptäckt av insikter](../../intelligent-services/customer-ai/user-guide/discover-insights.md).
