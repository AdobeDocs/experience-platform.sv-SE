---
title: Query Pro-läge
description: Lär dig hur du använder SQL-frågor i Adobe Experience Platform-gränssnittet för att generera diagram för dina anpassade instrumentpaneler.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Frågepro-läge {#query-pro-mode}

Frågeproläget är ett SQL-redigeringsbaserat arbetsflöde som guidar dig genom processen att generera insikter med anpassade SQL-frågor i Adobe Experience Platform-gränssnittet. Innan du kan generera insikter med anpassade SQL-frågor måste du [skapa en instrumentpanel](./overview.md#create-custom-dashboard).

## Skapa SQL {#compose-sql}

När du har valt att skapa en kontrollpanel med frågeproffsläge visas dialogrutan **[!UICONTROL Enter SQL]**. Välj en databas (datamodell för insikter) att fråga från listrutan och ange en lämplig fråga för datauppsättningen i frågeredigeraren.

>[!NOTE]
>
>Frågeproläget är endast tillgängligt för användare som har köpt Data Distiller SKU. [[!UICONTROL Guided design mode]](../../user-defined-dashboards.md) är tillgänglig för alla användare för att skapa insikter från en befintlig datamodell.

Mer information om användargränssnittselementen finns i [användarhandboken för Frågeredigeraren](../../../query-service/ui/user-guide.md#query-authoring).

![Dialogrutan [!UICONTROL Enter SQL] med listrutan Datamängd och ikonen för körning markerad har en ifylld SQL-fråga och fliken för frågeparametrar visas.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Frågeparametrar {#query-parameters}

Om du vill inkludera [globala](./filters/global-filter.md) eller [datumfilter](./filters/date-filter.md) måste **frågan** använda frågeparametrar. När du komponerar en sats i frågeproffsläge måste du ange exempelvärden om frågan använder frågeparametrar. Med exempelvärdena kan du köra SQL-satsen och skapa diagrammet. Observera att de exempelvärden du anger när du komponerar programsatsen ersätts med de faktiska värden du väljer för datumet eller det globala filtret vid körning.



>[!IMPORTANT]
>
>Om du vill använda ett globalt filter måste du placera en frågeparameter i SQL och sedan länka den frågeparametern till det globala filtret i widgetens disposition. I skärmbilden nedan används `CONSENT_VALUE_FILTER` i SQL som en frågeparameter för ett globalt filter. Mer information om hur du gör detta finns i [dokumentationen för det globala filtret](./filters/global-filter.md#enable-global-filter).

Om du vill köra frågan väljer du körningsikonen (![Körningsikonen.](/help/images/icons/play.png)). Frågeredigeraren visar resultatfliken. För att bekräfta konfigurationen och öppna widgetdispositionen väljer du **[!UICONTROL Select]**.

>[!TIP]
>
>Om frågan använder frågeparametrar kör du frågan en gång för att fylla i alla frågeparameternycklar som används i förväg. Frågan kommer att misslyckas, men gränssnittet visar automatiskt fliken Frågeparametrar och alla inkluderade nycklar. Lägg till lämpliga värden för dina nycklar.

![Dialogrutan [!UICONTROL Enter SQL] med SQL-indata, fliken Resultat och Markera.](../../images/customizable-insights/enter-sql-select.png)

## Fyll i widget {#populate-widget}

Widgetdispositionen är nu ifylld med kolumnerna från den SQL som körs. Instrumentpanelstypen anges i det övre vänstra hörnet, i det här fallet [!UICONTROL Manual SQL Entry]. Välj pennikonen (![En pennikon.](/help/images/icons/edit.png)) om du vill redigera SQL-koden.

>[!TIP]
>
>De tillgängliga attributen är kolumner som hämtas från den SQL som körs.

Om du vill skapa din widget använder du de attribut som listas i kolumnen [!UICONTROL Attributes]. Du kan använda sökfältet om du vill söka efter attribut eller bläddra i listan.

![Widgetdispositionen med metoden och attributkolumnen markerade.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Lägg till attribut {#add-attributes}

Om du vill lägga till ett attribut i widgeten väljer du plusikonen (![Ett plustecken-ikon.](/help/images/icons/add-circle.png)) bredvid ett attributnamn. Med listrutan som visas kan du lägga till ett attribut i diagrammet bland alternativen som bestäms av SQL-satsen. Olika diagramtyper har olika alternativ, till exempel en listruta för X- och Y-axlar.

I det här exemplet på ritstiftet är alternativen storlek och färg. Färgen bryter ned resultaten från donatchdiagrammet och storleken är det faktiska måttet som används. Lägg till ett attribut i fältet [!UICONTROL Color] om du vill dela upp resultaten i olika färger baserat på deras komposition i attributet.

>[!TIP]
>
>Välj upp- och nedpilen (![Ikonen med upp- och nedpilarna.](/help/images/icons/switch.png)) om du vill ändra X- och Y-axelns placering på stapel- eller linjediagram.

![Widgetdispositionen med listrutan Lägg till ikon och växlingspilarna markerade.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Om du vill ändra diagramtyp eller diagram för din widget väljer du bland de tillgängliga alternativen i listrutan [!UICONTROL Marks]. Alternativen är [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number] och [!UICONTROL Bar]. När du har valt det här alternativet genereras en förhandsvisningsbild av widgetens aktuella inställningar.

![Widgetdispositionen med widgetens förhandsvisning markerad.](../../images/customizable-insights/widget-preview.png)

## Widget-egenskaper {#properties}

Välj egenskapsikonen (![Egenskapsikonen.](/help/images/icons/properties.png)) till höger för att öppna egenskapspanelen. Ange ett namn för widgeten i textfältet **[!UICONTROL Widget title]** på panelen [!UICONTROL Properties]. Du kan också byta namn på olika aspekter av diagrammet.

>[!NOTE]
>
>Vilka specifika fält som är tillgängliga i egenskapssidlisten varierar beroende på vilken diagramtyp du redigerar.

![Widgetdispositionen med egenskapsikonen och namnfältet för widget markerat.](../../images/customizable-insights/widget-properties-title-text.png)

## Spara din widget {#save-widget}

När du sparar i widgetens disposition sparas widgeten lokalt på din instrumentpanel. Om du vill spara ditt arbete och återuppta det senare väljer du **[!UICONTROL Save]**. En bockikon under widgetens namn anger att widgeten har sparats. När du är nöjd med din widget kan du också välja **[!UICONTROL Save and close]** för att göra widgeten tillgänglig för alla andra användare med åtkomst till din instrumentpanel. Välj Avbryt om du vill avbryta ditt arbete och återgå till din anpassade kontrollpanel.

![Widgetdispositionen med Spara, Widget sparad och Spara och stäng markerad.](../../images/customizable-insights/insight-saved.png)

## Redigera kontrollpanelen och diagram {#edit}

Välj **[!UICONTROL Edit]** om du vill redigera hela instrumentpanelen eller någon av dina insikter. I redigeringsläget kan du ändra storlek på widgetar, redigera SQL-filer eller skapa och använda globala och tidsmässiga filter. Dessa filter begränsar de data som visas i widgetarna för kontrollpanelen. Det är ett bekvämt sätt att snabbt uppdatera och finjustera dina insikter för olika användningsfall.

![En anpassad instrumentpanel med Redigera markerat.](../../images/customizable-insights/edit-dashboard.png)

Välj **[!UICONTROL Add filter]** om du vill skapa en [[!UICONTROL Date filter]](#create-date-filter) eller en [[!UICONTROL Global filter]](#create-global-filter). När filtren har skapats är alla globala filter och datumfilter tillgängliga från [filterikonen](#select-global-filter) (![En filterikon.](/help/images/icons/filter.png)) på din instrumentpanel.

![En anpassad kontrollpanel med listrutan Lägg till filter markerad.](../../images/customizable-insights/add-filter.png)

## Redigera, duplicera eller ta bort en insikt

I handboken för den anpassade kontrollpanelen finns anvisningar om hur du [redigerar, duplicerar eller tar bort en befintlig widget](../../user-defined-dashboards.md#duplicate).

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skriver SQL-frågor i Adobe Experience Platform-gränssnittet för att generera diagram för dina anpassade instrumentpaneler. Därefter bör du lära dig att förbättra dina data ytterligare genom att [skapa ett datumfilter](./filters/date-filter.md) eller [skapa ett globalt filter](./filters/global-filter.md).

Du kan också lära dig mer om andra anpassade Insikter-funktioner, inklusive [de olika visningsalternativen för SQL-analyserade data](./view-more.md) eller hur du [visar SQL-data bakom anpassade insikter](./view-sql.md).
