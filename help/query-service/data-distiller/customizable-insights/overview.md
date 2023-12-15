---
title: Anpassningsbara insikter
description: Lär dig mer om användningsexempel, grundläggande funktioner och nödvändiga steg för att utveckla en anpassningsbar insiktspanel med Data Distiller. Upptäck hur funktionen för anpassningsbara insikter inom Data Distiller kan förbättra transparensen och få operativa insikter i olika dimensioner, som profiler, målgrupper, kampanjer, resor, berättiganden och samtycke.
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Anpassningsbara insikter

Skapa skräddarsydda rapportdatamodeller för att få djupare insikter, optimera strategier och anpassa analyser efter specifika affärsbehov med Data Distiller Customizable Insights. Använd funktionen för anpassningsbara insikter för att förbättra transparensen och få operativa insikter från era Adobe Experience Platform-data i olika dimensioner, som profiler, målgrupper, kampanjer, resor, berättiganden och samtycke. Denna funktion är en flexibel, anpassningsbar lösning som skräddarsyr organisationens rapporteringsdatamodeller för att passa just era affärsbehov.

Det här dokumentet innehåller användningsexempel, viktiga funktioner och nödvändiga steg för att utveckla en anpassningsbar insiktspanel med Data Distiller.

## Förutsättningar

I den här självstudien används användardefinierade kontrollpaneler för att visualisera data från din anpassade datamodell i plattformsgränssnittet. Se [användardefinierad dokumentation för kontrollpaneler](../../../dashboards/user-defined-dashboards.md) om du vill veta mer om funktionen.

## Komma igång

Data Distiller SKU krävs för att skapa en anpassad datamodell för dina rapportinsikter och för att utöka Real-Time CDP datamodeller som innehåller data från den nya plattformen. Se [packning](../../packaging.md), [skyddsräcken](../../guardrails.md#query-accelerated-store)och  [licensiering](../../data-distiller/license-usage.md) dokumentation som relaterar till Data Distiller SKU. Om du inte har Data Distiller SKU kontaktar du Adobe kundtjänstrepresentanten för mer information.

## Användningsexempel för anpassningsbara insikter {#use-cases}

Nedan visas vanliga användningsområden som effektivt kan hanteras via anpassningsbara insikter i Data Distiller.

### Genomskinlighet för profil- och målgruppsanvändning {#usage-transparency}

**Utmaning:** Så här bryter du ned nyckeltal (KPI) efter specifika kriterier som affärsenheter, lojalitetsstatus eller kundens livstidsvärde (CLTV).

**Customizable Insights Solution:** Data Distiller möjliggör utökning av datamodeller i Adobe Experience Platform, vilket underlättar [tillägg av anpassade profilattribut som CLTV](../../use-cases/customer-lifetime-value.md) eller lojalitetsstatus.

### Åtkomst till avvikelsespårning {#consent-anomaly-tracking}

**Utmaning:** Hur ni lägger in trendlinjerapporter för olika målgrupper och anpassar deras medgivandeattribut för kanaler som e-post, SMS och telefon.

**Customizable Insights Solution:** Rapportdatamodellen kan utökas för att spåra ändringar i medgivandeinställningarna över tid. Detta innebär att man skapar ytterligare faktabladen och dimensionstabeller för att trenda på medgivandeinställningar och schemaläggning [inkrementell datauppdatering](../../key-concepts/incremental-load.md).

### Optimera strategi för målgruppssegmentering {#optimize-audience-segmentation-strategy}

**Utmaning:** Hur man integrerar ML-modellgenererade benägenhetspoäng i målgruppernas KPI-rapporter.

**Customizable Insights Solution:** Med data från Distiller kan [benägenhetspoäng från anpassade ML-modeller](../../use-cases/propensity-score.md), vilket underlättar beräkningen av sammanlagda poäng på målgruppsnivå. Dessa data kan sedan rapporteras tillsammans med vanliga KPI:er.

### Målgruppsexpansion {#audience-expansion}

**Utmaning:** Hur man får in fler än bara antalet profiler i målgrupper överlappar rapporter och uppnår ytterligare demografiska data eller preferenser för att vägleda strategier för målgruppsexpansion.

**Customizable Insights Solution:** Genom att utöka rapportdatamodellen kan användarna lägga till ytterligare profilattribut, vilket förbättrar publikens överlappningsrapport med relevanta demografiska data och preferenser.

## Viktiga funktioner för att generera anpassningsbara insikter {#key-capabilities}

Bilden nedan visar flera viktiga funktioner för att skapa anpassningsbara insikter. Bland dessa funktioner finns:

1. **Datavisualiseringar:** Införliva visuella element som trender och stapeldiagram för en heltäckande bild av datatrender.
1. **Instrumentpanelsredigering:** Möjliggöra framtagning av anpassade kontrollpaneler som är skräddarsydda för specifika användningsfall, vilket ger en mer personaliserad och målinriktad analysupplevelse.
1. **Flexibel SQL-datamodellering:** Använd en mångsidig metod för SQL-datamodellering som gör det möjligt för användare att smidigt kombinera och hantera olika datauppsättningar, förbättra anpassningsförmågan och analysdjupet.
1. **Accelererad butik:** Implementera en accelererad butiksmekanism för att effektivt leverera sammanställda insikter via SQL, vilket ger smidig och snabb åtkomst till värdefull information.
1. **BI-anslutning:** Underlätta smidig integrering med vanliga verktyg för Business Intelligence (BI), som Power BI, Tableau, Looker och Apache Superset. Den här anslutningen garanterar kompatibilitet med olika BI-miljöer, vilket ger användarna flexibilitet att använda sina valverktyg för djupgående analyser och rapporter.

![Visual representations of the key capabilities of Data Distiller Customizable Insights.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Steg för att skapa anpassningsbara insikter {#steps-to-create}

Följ instruktionerna nedan för att utveckla en kontrollpanel för anpassningsbara insikter i Data Distiller.

1. **Ad hoc-frågeutforskande:** Börja med att köra ad hoc `SELECT` frågor för att utforska rådata på datarjön. På så sätt kan man experimentera direkt och experimentera med data och validera data där resultaten av frågorna inte lagras i datasjön.
1. **Användning av batchfråga:** Använd gruppfrågor för att [skapa schemalagda jobb](../../api/scheduled-queries.md#create-a-new-scheduled-query) för att generera insikter från sammanställda tabeller, vilket säkerställer en systematisk och automatiserad metod för databehandling. Kör gruppfrågor `INSERT TABLE AS SELECT` och `CREATE TABLE AS SELECT` frågor för att rensa, forma, manipulera och berika data. Resultatet av dessa frågor lagras i datasjön.
1. **Inläsning av aggregerade insikter:** Läs in genererade aggregerade insikter i det accelererade arkivet och använd SQL för att testa frågor, och säkerställ att datahämtningen är korrekt och effektiv. Så här lär du dig hur [skapa tillståndslösa frågor i det accelererade arkivet](../../api/accelerated-queries.md)finns i dokumentationen.
1. **Åtkomst och integrering:** Få smidig tillgång till de insikter som lagras i den accelererade butiken genom att integrera med Adobe Experience Platform [Användardefinierade kontrollpaneler](../../../dashboards/user-defined-dashboards.md) eller andra standardverktyg för Business Intelligence (BI). Dessa integreringar med tredjepartsklienter underlättar en sammanhängande och intuitiv upplevelse för användarna.

![En infografik som illustrerar de fyra stegen till Customizable Insights i Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Nästa steg

Genom att läsa det här dokumentet får du nu en bättre förståelse för användningsfall, viktiga funktioner och nödvändiga steg för att utveckla en anpassningsbar instrumentpanel för insikter med Data Distiller. Om du vill fortsätta lära dig mer om att skapa anpassade rapportdatamodeller kan du läsa [datamodellguide för rapportinsikter](./reporting-insights-data-model.md).
