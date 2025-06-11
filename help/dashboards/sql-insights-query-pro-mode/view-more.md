---
title: Visa mer
description: Lär dig mer om de olika visningsalternativen för SQL-analyserade data. På din anpassade kontrollpanel kan du visa resultaten av analysen i tabellform eller hämta bearbetade data i CSV-format.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 87675263b817a2026741d6bdd094010831d6ea28
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Visa mer {#view-more}

När du har skapat en [anpassad insikt](./overview.md) med [frågeproffsläget](./overview.md#query-pro-mode) kan du visa diagramdata i flera format. Du kan antingen visa ett tabellformulär eller exportera data i CSV-format eller via e-post.

## Resultat i tabellformat {#tabulated-results}

För varje diagram som skapats med frågeproffsläget via SQL kan du visa analysresultaten i tabellform i Experience Platform UI.

Välj ellipserna (`...`) på valfri widget från din anpassade kontrollpanel för att komma åt alternativen [!UICONTROL View more] och [!UICONTROL View SQL].

![En anpassad instrumentpanel med en insiktslistruta med ellipser och alternativen Visa mer och Visa SQL markerade.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Exportera {#export}

I dialogrutan **[!UICONTROL View more]** exporterar du tabelldata antingen genom att hämta en CSV-fil direkt eller genom att skicka en länk till e-postmeddelandet för säker hämtning senare.

>[!IMPORTANT]
>
>Din administratör måste ge dig behörighet **[!UICONTROL Export Dashboard Data]** för att komma åt exportalternativen. Om knappen [!UICONTROL Export] är nedtonad kontaktar du administratören. Mer information om kontrollpanelsbehörigheter finns i [Översikt över åtkomstkontroll](../../access-control/home.md).

>[!NOTE]
>
>Export med endast visualisering kräver inte behörighet [!UICONTROL Export Dashboard Data]. Du kan till exempel exportera bearbetade data från dina [anpassade instrumentpanelsinsikter i PDF-format](./export-pdf.md) eller från [instrumentpanelsinsikter för plattformsgränssnitt](../download.md).

### Hämta CSV {#download-csv}

I dialogrutan [!UICONTROL View more] väljer du **[!UICONTROL Export]** och sedan **[!UICONTROL Download CSV]** för att hämta diagramdata i CSV-format.

>[!NOTE]
>
>CSV-nedladdningen är begränsad till de första 500 posterna.

![En dialogruta som visar en förhandsvisning av dina insikter och de tabellariserade resultaten av din SQL som genererade insikten.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

### Skicka som e-post {#send-as-email}

Om du vill exportera mer än 500 poster markerar du **[!UICONTROL Export]** och väljer **[!UICONTROL Send as email]** i dialogrutan [!UICONTROL Export file]. Med det här alternativet skickas en nedladdningslänk säkert till din Adobe-relaterade e-postadress. Mottagarens namn och den registrerade e-postadressen för Adobe visas i avsnittet [!UICONTROL Recipients] i dialogrutan.

![Visa fler diagramdata med alternativen Exportera och Skicka som e-post markerade.](../images/sql-insights-query-pro-mode/send-as-email.png)

När du har valt [!UICONTROL Send as email] genererar Adobe en rapport och skickar ett e-postmeddelande till din registrerade Adobe-adress. E-postmeddelandet innehåller en säker nedladdningslänk som kräver autentisering via Experience Platform.

>[!NOTE]
>
>Du måste ladda ned rapporten inom 24 timmar efter länkgenereringen. Efter det upphör filen att gälla.

![Experience Platform-gränssnittet med dialogrutan Filgenerering slutförd som innehåller alternativet Hämta rapport visas.](../images/sql-insights-query-pro-mode/download-report.png)

För att skydda dina data är Adobe säkert värd för exporterade filer i stället för att skicka dem som bilagor. Åtkomst kräver autentisering via Experience Platform-gränssnittet, och Adobe verifierar att filen bara hämtas av den avsedda mottagaren.

Med den här metoden kan du exportera **upp till 10 000 poster** och säkerställa säker åtkomst till känsliga data.

## Sortera efter kolumn {#sort-column}

När du visar tabellresultat kan du använda sorteringsfunktionen för att sortera efter kolumn i stigande eller fallande ordning. Välj ellipserna (`...`) för en tabell från din anpassade kontrollpanel för att få åtkomst till alternativet [!UICONTROL View more].

![En anpassad kontrollpanel med en tabells listruta för ellipser och alternativet Visa fler markerat.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Du kan sortera kolumner genom att markera listrutan bredvid kolumnnamnet och sedan välja **[!UICONTROL Sort Ascending]** eller **[!UICONTROL Sort Descending]**.

>[!NOTE]
>
>Alternativen [!UICONTROL Sort Ascending] och [!UICONTROL Sort Descending] visas bara för kolumner som har konfigurerats med [sorteringsfunktionen](./overview.md#advanced-attributes).

![En listruta med tabellkolumner där alternativen Sortera stigande och Sortera fallande är markerade.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Ändra storlek på en kolumn {#resize-column}

Du kan ändra storlek på kolumner i tabellresultat för att förbättra läsbarheten för data. Välj ellipserna (`...`) för tabellen på din anpassade kontrollpanel för att få åtkomst till alternativet [!UICONTROL View more]. Använd listrutan bredvid kolumnnamnet för att ändra storlek på den och välj sedan **[!UICONTROL Resize column]**.

![En listruta för tabellkolumner med alternativet Ändra storlek markerat.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Markera reglaget och dra åt vänster eller höger för att justera kolumnstorleken efter behov.

![En tabell som visar kolumnstorleksfältet markerat.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Tabellsidnumrering {#table-pagination}

Sidnumrering används automatiskt för dina tabeller i funktionen [!UICONTROL View more], vilket eliminerar behovet av att manuellt ändra dina SQL-frågor. Den här funktionen gör att dina data presenteras i ett mer hanterbart format, vilket underlättar navigeringsprocessen i stora datauppsättningar.

Du kan se upp till 500 poster per sida. Om du vill navigera bland posterna använder du **[!UICONTROL >]** som finns längst ned på sidan.

![Resultat i tabellformat med resultat och sidnumrering markerade.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Nästa steg

När du har läst det här dokumentet vet du nu hur du kan visa tabellresultat från SQL-analysen i ditt anpassade diagram och hur du exporterar data på ett säkert sätt. Se SQL-dokumentet för att lära dig hur du [visar SQL bakom dina anpassade insikter](./view-sql.md).

Du kan också lära dig hur du genererar diagram från befintliga datamodeller i Adobe Experience Platform-gränssnittet med hjälp av [guiden för guidat designläge](../standard-dashboards.md).
