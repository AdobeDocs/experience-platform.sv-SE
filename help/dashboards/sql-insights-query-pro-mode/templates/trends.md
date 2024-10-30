---
title: Målgruppstrender
description: Lär dig att spåra och analysera målgruppsmått över tid med hjälp av kontrollpanelen Måltrender. Ange målgruppsfilter, analysera storlek och identitetstrender och exportera insikter för datadrivna beslut.
source-git-commit: 5fc786058a187b161a147a8bd361d19c5f35105d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Målgruppstrender

Analysera hur era målgrupper förändras över tid med visualiseringar av nyckeltal på kontrollpanelen [!UICONTROL Audience Trends]. Den här kontrollpanelen hjälper er att spåra trender som målgruppstillväxt, antalet identiteter och antalet enskilda identitetsprofiler, och ger er möjlighet att fatta datadrivna beslut. Genom att analysera dessa mätvärden kan marknadsförarna optimera strategier för målinriktning, förbättra målgruppsengagemanget och förfina sina segmenteringsinsatser för mer effektiva kampanjer.

## Filtrera målgrupper {#filter-audiences}

Börja analysen genom att använda det globala filtret för att välja de specifika målgrupperna och det datumintervall som du vill analysera. Välj filterikonen (![Filterikonen.](../../../images/icons/filter-icon-white.png)) för att öppna dialogrutan **[!UICONTROL Filter]** där du kan:

1. **Välj en målgrupp**: Välj den målgrupp som du vill analysera (i skärmbilden har **Amoxicillin**-målgruppen valts).
1. **Ange ett datumintervall**: Välj ett fördefinierat intervall i listrutan eller välj start- och slutdatum manuellt med hjälp av kalenderfälten.

![Dialogrutan Filter på kontrollpanelen Måltrender.](../../images/sql-insights-query-pro-mode/templates/audience-trends-filters.png)

När du har ställt in dina filter väljer du **[!UICONTROL Apply]** för att uppdatera instrumentpanelen. De filter du valt används och fokuserade insikter om utvalda målgrupper under en viss tidsperiod visas. Dina anpassade filter ser till att data är relevanta för dina analysmål.

![Kontrollpanelen Målgruppstrender med segmentfiltret Amoxicilin tillämpat och markerat.](../../images/sql-insights-query-pro-mode/templates/audience-trends-applied-filters.png)

## Tillgängliga trenddiagram för målgrupper {#available-charts}

Det finns tre huvuddiagram som hjälper er att förstå målgruppsmått över tid. För varje diagram kan du markera ellipsen (`...`) i det övre högra hörnet följt av [!UICONTROL View more] om du vill visa ett tabellformat för resultaten eller hämta data som en CSV-fil om du vill visa dem i ett kalkylblad. Mer information finns i [Visa mer guide](../view-more.md).

>[!TIP]
>
>Du kan hovra över ett visst datum i ett diagram om du vill visa antalet enskilda profiler i en dialogruta.

### Målgruppsstorlekstrender {#audience-size-trends}

Diagrammet **[!UICONTROL Audience size trends]** visar antalet profiler inom den valda målgruppen över tiden. Det hjälper till att spåra målgruppstillväxt eller -minskning. Du kan använda det här diagrammet för att övervaka hur engagemanget fungerar och förstå förändringar i målgruppens storlek.

![Trenddiagram för målgruppsstorlek.](../../images/sql-insights-query-pro-mode/templates/audience-size-trends-chart.png)

### Målgruppsidentitetstrender {#audience-identities-trends}

Diagrammet **[!UICONTROL Audience identities trends]** ger insikter om det totala antalet identiteter inom målgruppssegmentet. Använd det här diagrammet för att förstå hur unika identiteter bidrar till målgruppens totala storlek. Det ger en indikation på målgruppens stabilitet och engagemang.

![Trenddiagram för publikens identiteter.](../../images/sql-insights-query-pro-mode/templates/audience-identities-trends.png)

### Storlekstrender för en enda identitet {#single-identity-audience-size-trends}

Diagrammet **[!UICONTROL Single identity audience size trends]** visar antalet målgruppsmedlemmar med endast en identitet. Denna mätmetod är värdefull för att förstå målgruppens sammansättning, särskilt när det gäller identitetsskillnader, och hjälper till att mäta effekten av åtgärder för att sätta ihop identiteter.

![Storlekstrender för en enda identitetsmålgrupp.](../../images/sql-insights-query-pro-mode/templates/single-identity-audience-size-trends.png)

## Exportera insikter {#export-insights}

När du har analyserat mätvärdena och tillämpat relevanta filter kan du exportera data för vidare offlineanalys eller rapportering. Om du vill göra det väljer du **[!UICONTROL Export]** längst upp till höger i tabellen. Dialogrutan Skriv ut PDF visas. I den dialogrutan kan du spara visualiserade data som PDF eller skriva ut dem.

![Kontrollpanelen Målgruppstrender med Exportera markerad.](../../images/sql-insights-query-pro-mode/templates/audience-trends-export.png)

## Nästa steg

När du har läst det här dokumentet har du lärt dig att få värdefulla insikter om målgruppsbeteenden med tiden från kontrollpanelen **Målgruppstrender**. Om du vill veta mer om andra Distiller-mallar för data som kan hjälpa dig att fatta välgrundade beslut, optimera segmentering och förbättra engagemangsstrategier kan du läsa användargränssnittshandböckerna för [målgruppsjämförelsen](./comparison.md), [målgruppsidentitetsöverlappningar](./identity-overlaps.md) och [Avancerade målgruppsöverlappningar](./overlaps.md) .
