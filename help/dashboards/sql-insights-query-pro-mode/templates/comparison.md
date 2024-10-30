---
title: Målgruppsjämförelse
description: Lär dig hur du jämför viktiga mätvärden mellan olika målgruppsgrupper med hjälp av kontrollpanelen för målgruppsjämförelse. Ange målgruppsfilter, analysera trender och exportera insikter för datadrivna beslut
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Målgruppsjämförelse

Kontrollpanelen [!UICONTROL Audience comparison] jämför och kontrasterar viktiga målgruppsmått i en vy sida vid sida. Från den här kontrollpanelen kan du utföra en mängd åtgärder för att jämföra två målgruppsgrupper och analysera viktiga värden mellan dem. Sedan kan ni fatta datadrivna beslut om målgruppssegmentering och målinriktningsstrategier.

## Ange målgruppsjämförelser {#set-audience-comparisons}

Om du vill ha mer meningsfulla insikter och jämförelser kan du använda systemfiltren för att exakt rikta in dig på målgruppssegmenten och den tidsram du är intresserad av att analysera. Välj filterikonen (![Filterikonen.](../../../images/icons/filter-icon-white.png)) om du vill välja två olika målgrupper ([!UICONTROL Audience A] och [!UICONTROL Audience B]) och ange specifika parametrar för jämförelse.

![Dialogrutan Filter på kontrollpanelen för målgruppsjämförelse.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters.png)

Dialogrutan [!UICONTROL Filter] visas. Om du vill välja den första målgruppen som ska analyseras väljer du listrutan **[!UICONTROL Select Audience A]**. I det här exemplet har `California Patients` valts som målgrupp A. Den här målgruppen visas till vänster i jämförelsen när filtret har tillämpats.

Välj sedan en andra målgrupp att jämföra med [!UICONTROL Audience A] från listrutan **[!UICONTROL Select Audience B]**. I den här bilden har [!UICONTROL Users Consented to Email] valts som [!UICONTROL Audience B]. Den här målgruppen visas till höger på tavlan [!UICONTROL Audience comparison] när filtret har tillämpats.

### Justera datumintervall {#adjust-date-ranges}

Du kan också filtrera data efter specifika tidsperioder för att se hur dessa målgrupper fungerar eller förändras över ett anpassat datumintervall. Om du vill ange ett tidsintervall för att filtrera målgruppsdata efter en viss period väljer du start- och slutdatum i kalenderfälten.

Dialogrutan visar också hur många filter som används (i skärmbilden nedan används två filter: Målgrupp A och Målgrupp B, och i dag som ett datumintervall). Välj **[!UICONTROL Clear all]** om du vill ta bort alla filter som används.

När du har angett målgrupper och datumintervall väljer du **[!UICONTROL Apply]** för att uppdatera kontrollpanelen [!UICONTROL Audience comparison].

![Dialogrutan Filter på kontrollpanelen för målgruppsjämförelse med Använd markerad.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters-apply.png)

Kontrollpanelen visar nu de jämförande diagrammen som visas sida vid sida för varje målgrupp.

![Tavlan för publikjämförelse med flera diagram som jämför måtten för varje målgrupp.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-dashboard.png)

## Tillgängliga jämförelsetabeller {#available-charts}

<!-- Potentially could expand this section to include images of each widget.  -->

Kontrollpanelen innehåller flera diagram för att jämföra insikter:

- [[!UICONTROL Audience size]](../../guides/audiences.md#audience-size): Spåra enkelt storleken på varje målgrupp baserat på antalet profiler de innehåller. Denna mätmetod hjälper er att förstå omfattningen av de två målgrupper ni jämför.
- [!UICONTROL Audience identity breakdown]: Ett cirkeldiagram innehåller en beskrivning av den relativa sammansättningen av identiteter inom varje målgrupp. Du kan visa det totala antalet identiteter och undersöka hur olika identifierare (som e-post eller CRM-ID) bidrar till det totala antalet. I det här diagrammet får du hjälp att förstå hur varje målgrupp är sammansatt utifrån identitetstyper. Håll pekaren över ett avsnitt i cirkeldiagrammet för att se ett exakt antal identiteter.
- [[!UICONTROL Audience size trend]](../../guides/audiences.md#audience-size-trend): Det här diagrammet visar storlekstrender över tid för den valda målgruppen. Använd dessa diagram för att visualisera hur storleken på varje målgrupp har ändrats under en viss tidsperiod, med toppar och dalar som anger perioder av tillväxt eller minskning av antalet profiler.
- [[!UICONTROL Audience size change trend]](../../guides/audiences.md#audience-size-change-trend): Det här diagrammet visar trender för storleksändring för den valda målgruppen. Det visar hur mycket publikstorleken har ökat eller minskat över tiden och gör det möjligt att identifiera betydande förändringar eller trender i målgruppen.

>[!NOTE]
>
>Diagrammen [!UICONTROL Audience size trend] och [!UICONTROL Audience size change trend] hjälper dig att spåra och jämföra både den absoluta storleken och variationer i storlek mellan två målgrupper under en angiven period. Den här informationen gör det enklare att förstå mönster och faktorer som påverkar publikens ändringar.

## Exportera insikter {#export-insights}

När du har tillämpat filter och analyserat målgrupperna kan du exportera data för ytterligare offline-analys eller rapportering. Om du vill exportera dina insikter väljer du **[!UICONTROL Export]** längst upp till höger i tabellen. Dialogrutan Skriv ut PDF visas. I den här dialogrutan kan du spara de data som visas i PDF eller skriva ut dem som en tabell.

Välj **[!UICONTROL Templates]** för att återgå till översikten över [!UICONTROL Template].

![Vyn Avancerad publik överlappar vyn med mallar markerade.](../../images/sql-insights-query-pro-mode/templates/navigation.png)

## Nästa steg

När du har läst det här dokumentet har du lärt dig att jämföra nyckeltal mellan olika målgrupper med hjälp av **instrumentpanelen för målgruppsjämförelse**. Om du vill fortsätta att förbättra målgruppssegmenteringen och målgruppsstrategierna kan du utforska andra Data Distiller-mallar som ger ytterligare insikter. Se [Målgruppstrender](./trends.md), [Överlappar av målgruppsidentitet](./identity-overlaps.md) och [Överlappar av avancerad målgrupp](./overlaps.md) användargränssnittsguider som ytterligare förbättrar ditt beslutsfattande och optimerar insatser för engagemang.

