---
title: Visa mer
description: Lär dig mer om de olika visningsalternativen för SQL-analyserade data. På din anpassade kontrollpanel kan du visa resultaten av analysen i tabellform eller hämta bearbetade data i CSV-format.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 1ef8208ccde2f44b6c5188bd5b9a57ff876da30f
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Visa mer {#view-more}

När du har skapat en [anpassad insikt](../sql-insights/overview.md) med [frågeproffsläge](./overview.md) kan du visa diagramdata i olika format. Du kan antingen visa en tabellform av resultaten eller hämta data som en CSV-fil för visning i ett kalkylblad.

## Resultat i tabellformat {#tabulated-results}

För varje diagram som skapats med frågeproffsläget via SQL kan du visa analysresultaten i tabellform i användargränssnittet för Experience Platform.

Välj ellipserna (`...`) på valfri widget från din anpassade kontrollpanel för att komma åt alternativen [!UICONTROL View more] och [!UICONTROL View SQL].

![En anpassad instrumentpanel med en insiktslistruta med ellipser och alternativen Visa mer och Visa SQL markerade.](../../images/sql-insights/ellipses-dropdown.png)

## Hämta CSV {#download-csv}

Funktionen [!UICONTROL View more] visar specifika datapunkter för diagrammet i tabellform. Om du vill förenkla processen för delning och hantering av data kan du hämta bearbetade data i CSV-format från den här dialogrutan. Välj **[!UICONTROL Download CSV]** om du vill hämta dina data.

>[!NOTE]
>
>CSV-nedladdningen är begränsad till de första 500 posterna.

![En dialogruta som visar en förhandsvisning av dina insikter och de tabellariserade resultaten av din SQL som genererade insikten.](../../images/query-pro-mode/view-more-download-csv.png)

## Sortera efter kolumn {#sort-column}

När du visar tabellresultat kan du använda sorteringsfunktionen för att sortera efter kolumn i stigande eller fallande ordning. Välj ellipserna (`...`) för en tabell från din anpassade kontrollpanel för att få åtkomst till alternativet [!UICONTROL View more].

![En anpassad kontrollpanel med en tabells listruta för ellipser och alternativet Visa fler markerat.](../../images/query-pro-mode/advanced-ellipses-dropdown.png)

Du kan sortera kolumner genom att markera listrutan bredvid kolumnnamnet och sedan välja **[!UICONTROL Sort Ascending]** eller **[!UICONTROL Sort Descending]**.

>[!NOTE]
>
>Alternativen [!UICONTROL Sort Ascending] och [!UICONTROL Sort Descending] visas bara för kolumner som har konfigurerats med [sorteringsfunktionen](./overview.md#advanced-attributes).

![En listruta med tabellkolumner där alternativen Sortera stigande och Sortera fallande är markerade.](../../images/query-pro-mode/advanced-sort-dropdown.png)

## Ändra storlek på en kolumn {#resize-column}

Du kan ändra storlek på kolumner i tabellresultat för att förbättra läsbarheten för data. Välj ellipserna (`...`) för tabellen på din anpassade kontrollpanel för att få åtkomst till alternativet [!UICONTROL View more]. Använd listrutan bredvid kolumnnamnet för att ändra storlek på den och välj sedan **[!UICONTROL Resize column]**.

![En listruta för tabellkolumner med alternativet Ändra storlek markerat.](../../images/query-pro-mode/advanced-resize-dropdown.png)

Markera reglaget och dra åt vänster eller höger för att justera kolumnstorleken efter behov.

![En tabell som visar kolumnstorleksfältet markerat.](../../images/query-pro-mode/advanced-resize-column.png)

## Tabellsidnumrering {#table-pagination}

Sidnumrering används automatiskt för dina tabeller i funktionen [!UICONTROL View more], vilket eliminerar behovet av att manuellt ändra dina SQL-frågor. Den här funktionen gör att dina data presenteras i ett mer hanterbart format, vilket underlättar navigeringsprocessen i stora datauppsättningar.

Du kan se upp till 500 poster per sida. Om du vill navigera bland posterna använder du **[!UICONTROL >]** som finns längst ned på sidan.

![Resultat i tabellformat med resultat och sidnumrering markerade.](../../images/query-pro-mode/advanced-table-pagination.png)

## Nästa steg

När du har läst det här dokumentet vet du nu hur du visar tabellresultaten från SQL-analysen för ditt anpassade diagram och hämtar data som en CSV-fil. Se SQL-dokumentet för att lära dig hur du [visar SQL bakom dina anpassade insikter](./view-more.md).

Du kan också lära dig hur du genererar diagram från befintliga datamodeller i Adobe Experience Platform-gränssnittet med hjälp av [guiden för guidat designläge](../../user-defined-dashboards.md).
