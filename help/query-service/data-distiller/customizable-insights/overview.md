---
title: Anpassningsbara insikter
description: Lär dig mer om användningsexempel, grundläggande funktioner och nödvändiga steg för att utveckla en anpassningsbar insiktspanel med Data Distiller. Upptäck hur funktionen för anpassningsbara insikter inom Data Distiller kan förbättra transparensen och få operativa insikter i olika dimensioner, som profiler, målgrupper, kampanjer, resor, berättiganden och samtycke.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Anpassningsbara insikter

Skapa skräddarsydda rapportdatamodeller för att få djupare insikter, optimera strategier och anpassa analyser efter specifika affärsbehov med Data Distiller Customizable Insights. Använd funktionen för anpassningsbara insikter för att förbättra transparensen och få operativa insikter från era Adobe Experience Platform-data i olika dimensioner, som profiler, målgrupper, kampanjer, resor, berättiganden och samtycke. Denna funktion är en flexibel, anpassningsbar lösning som skräddarsyr organisationens rapporteringsdatamodeller för att passa just era affärsbehov.

Om du vill [visualisera dina anpassningsbara insikter](../../../dashboards/data-distiller/overview.md) kan du använda [frågeproffsläget](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) för att utföra komplexa analyser med anpassade SQL-frågor och omvandla dina data till lätttolkade diagram. Använd frågeproffsläget för att skapa skräddarsydda insikter och visualiseringar på kontrollpanelerna och ta hänsyn till både tekniska och icke-tekniska målgrupper genom att ladda ned insikter som CSV-filer.

Det här dokumentet innehåller användningsexempel, viktiga funktioner och nödvändiga steg för att utveckla en anpassningsbar insiktspanel med Data Distiller.

## Förhandskrav

I den här självstudien används användardefinierade kontrollpaneler för att visualisera data från din anpassade datamodell i plattformsgränssnittet. Mer information om den här funktionen finns i [användardefinierad dokumentation för kontrollpaneler](../../../dashboards/user-defined-dashboards.md).

## Komma igång

Data Distiller SKU krävs för att skapa en anpassad datamodell för dina rapportinsikter och för att utöka Real-Time CDP datamodeller som innehåller data från den nya plattformen. Se dokumentationen för [paketering](../../packaging.md), [skyddsutkast](../../guardrails.md#query-accelerated-store) och [licensiering](../../data-distiller/license-usage.md) som gäller Data Distiller SKU. Om du inte har Data Distiller SKU kontaktar du Adobe kundtjänstrepresentanten för mer information.

## Användningsexempel för anpassningsbara insikter {#use-cases}

Nedan visas vanliga användningsområden som effektivt kan hanteras via anpassningsbara insikter i Data Distiller.

### Genomskinlighet för profil- och målgruppsanvändning {#usage-transparency}

**Problem:** Så här bryter du ned nyckeltal (KPI) efter specifika kriterier som affärsenheter, lojalitetsstatus eller kundens livstidsvärde (CLTV).

**Anpassningsbar Insights-lösning:** Med Data Distiller kan du utöka rapporteringsdatamodeller i Adobe Experience Platform, vilket underlättar för [att lägga till anpassade profilattribut som CLTV](../../use-cases/customer-lifetime-value.md) eller lojalitetsstatus.

### Åtkomst till avvikelsespårning {#consent-anomaly-tracking}

**Utmaning:** Så här tillämpar du målgruppsöverlappnings- och storlekstrendlinjerapporter på anpassade medgivandeattribut för kanaler som e-post, SMS och telefon.

**Anpassningsbar Insights-lösning:** Rapportdatamodellen kan utökas för att spåra ändringar i medgivandeinställningarna över tid. Detta innebär att du skapar ytterligare fakt- och dimensionstabeller för att trendanpassa medgivandeinställningar och schemalägga [inkrementell datauppdatering](../../key-concepts/incremental-load.md).

### Optimera strategi för målgruppssegmentering {#optimize-audience-segmentation-strategy}

**Utmaning:** Så här integrerar du ML-modellgenererade benägenhetspoäng i målgruppernas KPI-rapporter.

**Anpassningsbar Insights-lösning:** Med Data Distiller kan du inkludera [benägenhetspoäng från anpassade ML-modeller](../../use-cases/propensity-score.md), vilket underlättar beräkningen av aggregerade poäng på målgruppsnivå. Dessa data kan sedan rapporteras tillsammans med vanliga KPI:er.

### Målgruppsexpansion {#audience-expansion}

**Utmaning:** Så här förvärvar du fler än bara antalet profiler i målgrupper överlappar rapporter och uppnår ytterligare demografiska data eller inställningar som kan vägleda strategier för målgruppsexpansion.

**Anpassningsbar Insights-lösning:** Genom att utöka rapportdatamodellen kan användarna lägga till ytterligare profilattribut, vilket förbättrar publikens överlappningsrapport med relevanta demografiska data och inställningar.

## Viktiga funktioner för att generera anpassningsbara insikter {#key-capabilities}

Bilden nedan visar flera viktiga funktioner för att skapa anpassningsbara insikter. Bland dessa funktioner finns:

1. **Datavisualiseringar:** Innehåller visuella element som trender och stapeldiagram för en heltäckande bild av datatrender.
1. **Instrumentpanelsredigering:** Gör det möjligt att skapa anpassade instrumentpaneler som är anpassade till specifika användningsfall, vilket ger en mer personaliserad och målinriktad analysupplevelse.
1. **Flexibel SQL-datamodellering:** Använd en mångsidig metod för SQL-datamodellering som gör det möjligt för användare att sömlöst kombinera och ändra olika datauppsättningar, förbättra anpassningsförmågan och analytiskt djup.
1. **Accelerated store:** Implementera en accelererad butiksmekanism för att effektivt hantera aggregerade insikter via SQL, vilket ger smidig och snabb åtkomst till värdefull information.
1. **BI-anslutning:** Underlättar smidig integrering med vanliga Business Intelligence-verktyg (BI), inklusive Power BI, Tableau, Looker och Apache Superset. Den här anslutningen garanterar kompatibilitet med olika BI-miljöer, vilket ger användarna flexibilitet att använda sina valverktyg för djupgående analyser och rapporter.

![Visuella representationer av nyckelfunktionerna i Data Distiller Customizable Insights.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Steg för att skapa anpassningsbara insikter {#steps-to-create}

Följ instruktionerna nedan för att utveckla en kontrollpanel för anpassningsbara insikter i Data Distiller.

1. **Ad hoc-frågeutforskande:** Börja med att köra ad hoc `SELECT` -frågor för att utforska raw-data i datasjön. På så sätt kan man experimentera direkt och experimentera med data och validera data där resultaten av frågorna inte lagras i datasjön.
1. **Använd batchfråga:** Använd batchfrågor för att [skapa schemalagda jobb](../../api/scheduled-queries.md#create-a-new-scheduled-query) för att generera sammanställda insikter, vilket ger en systematisk och automatiserad databearbetning. Gruppfrågor kör `INSERT TABLE AS SELECT`- och `CREATE TABLE AS SELECT`-frågor för att rensa, forma, manipulera och förbättra data. Resultatet av dessa frågor lagras i datasjön.
1. **Aggregerade insikter läses in:** Läs in de genererade aggregerade insikterna i det accelererade arkivet och använd SQL för att testa frågor, och se till att data hämtas på ett korrekt och effektivt sätt. Mer information om hur du [ställer tillståndslösa frågor till det accelererade arkivet](../../api/accelerated-queries.md) finns i dokumentationen.
1. **Åtkomst och integrering:** Få tillgång till insikter som lagras i den accelererade butiken sömlöst genom att integrera med Adobe Experience Platform [användardefinierade Dashboards](../../../dashboards/user-defined-dashboards.md) eller andra BI-verktyg (Business Intelligence preferred tools). Dessa integreringar med tredjepartsklienter underlättar en sammanhängande och intuitiv upplevelse för användarna.

![En infografik som illustrerar de fyra stegen till Anpassningsbara insikter i Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för användningsfall, viktiga funktioner och nödvändiga steg för att utveckla en anpassningsbar instrumentpanel för insikter med Data Distiller. Mer information om hur du skapar anpassade rapportdatamodeller finns i [guiden ](./reporting-insights-data-model.md) om datamodellen för rapportinsikter.
