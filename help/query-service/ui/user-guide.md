---
keywords: Experience Platform;home;popular topics;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Användarhandbok för Frågeredigeraren
topic: query editor
description: Frågeredigeraren är ett interaktivt verktyg som tillhandahålls av Adobe Experience Platform Query Service, som gör att du kan skriva, validera och köra frågor för kundupplevelsedata i användargränssnittet i Experience Platform. Frågeredigeraren har stöd för att utveckla frågor för analys och datautforskande, och gör att du kan köra interaktiva frågor i utvecklingssyfte samt icke-interaktiva frågor för att fylla i datauppsättningar i Experience Platform.
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# [!DNL Query Editor] användarhandbok

[!DNL Query Editor] är ett interaktivt verktyg från Adobe Experience Platform [!DNL Query Service]som gör att du kan skriva, validera och köra frågor om kundupplevelsedata i [!DNL Experience Platform] användargränssnittet. [!DNL Query Editor] har stöd för utveckling av frågor för analys och datautforskande, och gör att du kan köra interaktiva frågor i utvecklingssyfte samt icke-interaktiva frågor för att fylla i datauppsättningar i [!DNL Experience Platform].

Mer information om begrepp och funktioner i [!DNL Query Service]finns i [frågetjänstens översikt][query-service-overview]. Mer information om hur du navigerar i användargränssnittet för frågetjänsten [!DNL Platform]finns i [Översikt över][query-service-ui]användargränssnittet för frågetjänsten.

## Komma igång

[!DNL Query Editor] erbjuder flexibel körning av frågor genom att ansluta till [!DNL Query Service], och frågor körs bara när den här anslutningen är aktiv.

### Ansluter till [!DNL Query Service]

[!DNL Query Editor] tar några sekunder att initiera och ansluta till [!DNL Query Service] när den öppnas. Konsolen talar om när den är ansluten, så som visas nedan. Om du försöker köra en fråga innan redigeraren har anslutit, fördröjs körningen tills anslutningen är klar.

![Bild](../images/queries/query-editor-overview/initializing-connection.png)

### Hur frågor körs från [!DNL Query Editor]

Frågor som körs från [!DNL Query Editor] kör interaktivt. Det innebär att om du stänger webbläsaren eller navigerar bort så avbryts frågan. Detta gäller även för frågor som skapas för att generera datauppsättningar från frågeutdata.

## Frågeredigering med [!DNL Query Editor]

Med [!DNL Query Editor]kan du skriva, köra och spara frågor om kundupplevelsedata. Alla frågor som körs i [!DNL Query Editor], eller sparas, är tillgängliga för alla användare i organisationen som har tillgång till [!DNL Query Service].

### Komma åt [!DNL Query Editor]

I [!DNL Experience Platform] användargränssnittet klickar du **[!UICONTROL Queries]** på den vänstra navigeringsmenyn för att öppna [!DNL Query Service] arbetsytan. Klicka sedan på **[!UICONTROL Create Query]** längst upp till höger på skärmen för att börja skriva frågor. Den här länken är tillgänglig från alla sidor på [!DNL Query Service] arbetsytan.

![Bild](../images/queries/query-editor-overview/create-query.png)

### Skriver frågor

[!UICONTROL Query Editor] är organiserat för att göra det så enkelt att skriva frågor som möjligt. Skärmbilden nedan visar hur redigeraren visas i användargränssnittet med knappen **Spela upp** och SQL-inmatningsfältet markerat.

![Bild](../images/queries/query-editor-overview/editor.png)

För att minimera utvecklingstiden rekommenderar vi att du utvecklar dina frågor med begränsningar för antalet rader som returneras. Exempel, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. När du har verifierat att frågan skapar det förväntade resultatet tar du bort gränserna och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata.

### Skrivverktyg i [!DNL Query Editor]

- **Automatisk syntaxmarkering:** Gör det enklare att läsa och ordna SQL.

![Bild](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-nyckelord slutförs automatiskt:** Börja skriva frågan, använd piltangenterna för att navigera till önskad term och tryck på **Retur**.

![Bild](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabell och fält har fyllts i automatiskt:** Börja skriva det tabellnamn du vill `SELECT` komma från, använd sedan piltangenterna för att navigera till tabellen du söker efter och tryck på **Retur**. När en tabell är markerad identifieras fält i tabellen automatiskt.

![Bild](../images/queries/query-editor-overview/tables-auto.png)

### Felidentifiering

[!DNL Query Editor] validerar automatiskt en fråga medan du skriver den, vilket ger generisk SQL-validering och specifik körningsvalidering. Om en röd understrykning visas under frågan (som bilden nedan visar) representerar den ett fel i frågan.

![Bild](../images/queries/query-editor-overview/syntax-error-highlight.png)

När fel upptäcks kan du visa de specifika felmeddelandena genom att hovra över SQL-koden.

![Bild](../images/queries/query-editor-overview/linting-error.png)

### Frågeinformation

När du visar en fråga i [!DNL Query Editor]innehåller panelen verktyg för att hantera den valda **[!UICONTROL Query Details]** frågan.

![Bild](../images/queries/query-editor-overview/query-details.png)

På den här panelen kan du generera en utdatauppsättning direkt från användargränssnittet, ta bort eller namnge den visade frågan och visa SQL-koden i ett format som är enkelt att kopiera på **[!UICONTROL SQL Query]** fliken. På den här panelen visas även användbara metadata som den senaste gången frågan ändrades och vem som ändrade den, om tillämpligt. Om du vill generera en datauppsättning klickar du på **[!UICONTROL Output Dataset]**. Dialogrutan **[!UICONTROL Output Dataset]** visas. Ange ett namn och en beskrivning och klicka sedan på **[!UICONTROL Run Query]**. Den nya datauppsättningen visas på **[!UICONTROL Datasets]** fliken i [!DNL Query Service] användargränssnittet på [!DNL Platform].

### Sparar frågor

[!DNL Query Editor] innehåller en funktion för att spara som gör att du kan spara en fråga och arbeta med den senare. Om du vill spara en fråga klickar du **[!UICONTROL Save]** i det övre högra hörnet av [!DNL Query Editor]. Innan en fråga kan sparas måste du ange ett namn för frågan med hjälp av **[!UICONTROL Query Details]** panelen.

### Söka efter tidigare frågor

Alla frågor som körs från [!DNL Query Editor] hämtas i loggtabellen. Du kan använda sökfunktionen på fliken **[!UICONTROL Log]** för att hitta frågekörningar. Sparade frågor visas på **[!UICONTROL Browse]** fliken.

Mer information finns i översikten över användargränssnittet för [frågetjänsten][query-service-ui] .

>[!NOTE]
>
>Frågor som inte körs sparas inte av loggen. För att frågan ska vara tillgänglig i [!DNL Query Service]måste den köras eller sparas i [!DNL Query Editor].

## Köra frågor med Frågeredigeraren

Om du vill köra en fråga i [!DNL Query Editor]kan du ange SQL i redigeraren eller läsa in en tidigare fråga från *loggen* eller **[!UICONTROL Browse]** fliken och klicka på **Spela upp**. Status för frågekörning visas på fliken **[!UICONTROL Console]** nedan och utdata visas på **[!UICONTROL Results]** fliken.

### Konsol

Konsolen ger information om status och funktion för [!DNL Query Service]. Konsolen visar anslutningsstatus till [!DNL Query Service], frågeåtgärder som körs och eventuella felmeddelanden som är ett resultat av dessa frågor.

![Bild](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Konsolen visar bara fel som uppstått när en fråga kördes. Frågevalideringsfel visas inte innan en fråga körs.

### Frågeresultat

När en fråga är klar visas resultatet på **[!UICONTROL Results]** fliken bredvid **[!UICONTROL Console]** fliken. I den här vyn visas frågans tabellutdata med upp till 100 rader. I den här vyn kan du verifiera att frågan ger förväntat resultat. Om du vill generera en datauppsättning med frågan tar du bort begränsningar för returnerade rader och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata. I självstudiekursen [][query-service-create-datasets] om att generera datauppsättningar finns instruktioner om hur du genererar en datauppsättning från frågeresultat i [!DNL Query Editor].

![Bild](../images/queries/query-editor-overview/query-results.png)

## Köra frågor med [!DNL Query Service] självstudievideo

I följande video visas hur du kör frågor i Adobe Experience Platform-gränssnittet och i en PSQL-klient. Dessutom visas om du använder enskilda egenskaper i ett XDM-objekt, använder funktioner som definieras av Adobe och använder CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nästa steg

Nu när du vet vilka funktioner som är tillgängliga i [!DNL Query Editor] och hur du navigerar i programmet kan du börja skapa egna frågor direkt i [!DNL Platform]. Mer information om hur du kör SQL-frågor mot datauppsättningar i [!DNL Data Lake]finns i guiden om [att köra frågor][query-service-running-queries]. Exempel på SQL-frågor som du kan använda för att arbeta med Adobe Analytics- och Adobe Target-data finns i [exempelfrågereferensen][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
