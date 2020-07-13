---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Frågeredigeringsguide för Adobe Experience Platform Query Service
topic: query editor
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---


# Användarhandbok för Frågeredigeraren

Frågeredigeraren är ett interaktivt verktyg som tillhandahålls av Adobe Experience Platform Query Service, som gör att du kan skriva, validera och köra frågor för kundupplevelsedata i användargränssnittet i Experience Platform. Frågeredigeraren har stöd för att utveckla frågor för analys och datautforskande, och gör att du kan köra interaktiva frågor i utvecklingssyfte samt icke-interaktiva frågor för att fylla i datauppsättningar i Experience Platform.

Mer information om begrepp och funktioner i tjänsten Query Service finns i Översikt över [][query-service-overview]tjänsten Query. Mer information om hur du navigerar i användargränssnittet för frågetjänsten i Platform finns i [Översikt över][query-service-ui]användargränssnittet för frågetjänsten.

## Komma igång

Frågeredigeraren erbjuder flexibel körning av frågor genom anslutning till frågetjänsten, och frågor körs bara när den här anslutningen är aktiv.

### Ansluter till frågetjänsten

Frågeredigeraren tar några sekunder att initiera och ansluta till frågetjänsten när den öppnas. Konsolen talar om när den är ansluten, så som visas nedan. Om du försöker köra en fråga innan redigeraren har anslutit, fördröjs körningen tills anslutningen är klar.

![Bild](../images/queries/query-editor-overview/initializing-connection.png)

### Hur frågor körs från frågeredigeraren

Frågor som körs från Frågeredigeraren körs interaktivt. Det innebär att om du stänger webbläsaren eller navigerar bort så avbryts frågan. Detta gäller även för frågor som skapas för att generera datauppsättningar från frågeutdata.

## Frågeredigering med Frågeredigeraren

Med Frågeredigeraren kan du skriva, köra och spara frågor om kundupplevelsedata. Alla frågor som körs i Frågeredigeraren, eller sparas, är tillgängliga för alla användare i organisationen som har tillgång till tjänsten Query Service.

### Åtkomst till frågeredigeraren

I användargränssnittet för Experience Platform klickar du på **Frågor** i den vänstra navigeringsmenyn för att öppna arbetsytan för frågetjänsten. Klicka sedan på **Skapa fråga** längst upp till höger på skärmen för att börja skriva frågor. Den här länken är tillgänglig från någon av sidorna på arbetsytan för frågetjänsten.

![Bild](../images/queries/query-editor-overview/create-query.png)

### Skriver frågor

Frågeredigeraren är organiserad så att det blir så enkelt att skriva frågor som möjligt. Skärmbilden nedan visar hur redigeraren visas i användargränssnittet med knappen **Spela upp** och SQL-inmatningsfältet markerat.

![Bild](../images/queries/query-editor-overview/editor.png)

För att minimera utvecklingstiden rekommenderar vi att du utvecklar dina frågor med begränsningar för antalet rader som returneras. Exempel, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. När du har verifierat att frågan skapar det förväntade resultatet tar du bort gränserna och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata.

### Skrivverktyg i Frågeredigeraren

- **Automatisk syntaxmarkering:** Gör det enklare att läsa och ordna SQL.

![Bild](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-nyckelord slutförs automatiskt:** Börja skriva frågan, använd piltangenterna för att navigera till önskad term och tryck på **Retur**.

![Bild](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabell och fält har fyllts i automatiskt:** Börja skriva det tabellnamn du vill `SELECT` komma från, använd sedan piltangenterna för att navigera till tabellen du söker efter och tryck på **Retur**. När en tabell är markerad identifieras fält i tabellen automatiskt.

![Bild](../images/queries/query-editor-overview/tables-auto.png)

### Felidentifiering

Frågeredigeraren validerar automatiskt en fråga medan du skriver den, vilket ger generisk SQL-validering och specifik körningsvalidering. Om en röd understrykning visas under frågan (som bilden nedan visar) representerar den ett fel i frågan.

![Bild](../images/queries/query-editor-overview/syntax-error-highlight.png)

När fel upptäcks kan du visa de specifika felmeddelandena genom att hovra över SQL-koden.

![Bild](../images/queries/query-editor-overview/linting-error.png)

### Frågeinformation

När du visar en fråga i Frågeredigeraren innehåller panelen *Frågedetaljer* verktyg för att hantera den valda frågan.

![Bild](../images/queries/query-editor-overview/query-details.png)

På den här panelen kan du generera en utdatauppsättning direkt från användargränssnittet, ta bort eller namnge den visade frågan och visa SQL-koden i ett format som är enkelt att kopiera på fliken *SQL-fråga* . På den här panelen visas även användbara metadata som den senaste gången frågan ändrades och vem som ändrade den, om tillämpligt. Klicka på **Utdatauppsättning** om du vill skapa en datauppsättning. Dialogrutan *Utdatauppsättning* visas. Ange ett namn och en beskrivning och klicka sedan på **Kör fråga**. Den nya datauppsättningen visas på fliken *Datauppsättningar* i användargränssnittet för frågetjänsten i Platform.

### Sparar frågor

Frågeredigeraren innehåller en funktion för att spara en fråga och arbeta med den senare. Om du vill spara en fråga klickar du på **Spara** i det övre högra hörnet i Frågeredigeraren. Innan en fråga kan sparas måste ett namn anges för frågan med hjälp av panelen *Frågeinformation* .

### Söka efter tidigare frågor

Alla frågor som körs från Frågeredigeraren hämtas i loggtabellen. Du kan använda sökfunktionen på fliken *Logg* för att hitta frågekörningar. Sparade frågor visas på fliken *Bläddra* .

Mer information finns i översikten över användargränssnittet för [frågetjänsten][query-service-ui] .

>[!NOTE]
>
>Frågor som inte körs sparas inte av loggen. För att frågan ska vara tillgänglig i frågetjänsten måste den köras eller sparas i frågeredigeraren.

## Köra frågor med Frågeredigeraren

Om du vill köra en fråga i Frågeredigeraren kan du ange SQL i redigeraren eller läsa in en tidigare fråga från *fliken Logg* eller *Bläddra* och klicka på **Spela upp**. Status för frågekörning visas på fliken *Konsol* nedan och utdata visas på fliken *Resultat* .

### Konsol

Konsolen ger information om status och funktion för frågetjänsten. Konsolen visar anslutningsstatus till frågetjänsten, frågeåtgärder som körs och eventuella felmeddelanden som är ett resultat av dessa frågor.

![Bild](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Konsolen visar bara fel som uppstått när en fråga kördes. Frågevalideringsfel visas inte innan en fråga körs.

### Frågeresultat

När en fråga har slutförts visas resultaten på fliken *Resultat* bredvid fliken *Konsol* . I den här vyn visas frågans tabellutdata med upp till 100 rader. I den här vyn kan du verifiera att frågan ger förväntat resultat. Om du vill generera en datauppsättning med frågan tar du bort begränsningar för returnerade rader och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata. I självstudiekursen [][query-service-create-datasets] om att generera datauppsättningar finns instruktioner om hur du genererar en datauppsättning från frågeresultat i Frågeredigeraren.

![Bild](../images/queries/query-editor-overview/query-results.png)

## Köra frågor med självstudievideo om frågetjänsten

I följande video visas hur du kör frågor i gränssnittet Adobe Experience Platform och i en PSQL-klient. Dessutom visas hur du använder enskilda egenskaper i ett XDM-objekt, använder Adobe-definierade funktioner och använder CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nästa steg

Nu när du vet vilka funktioner som är tillgängliga i Frågeredigeraren och hur du navigerar i programmet kan du börja skapa egna frågor direkt i Platform. Mer information om hur du kör SQL-frågor mot datauppsättningar i Data Lake finns i guiden om hur du [kör frågor][query-service-running-queries]. SQL-frågor som du kan använda som exempel när du arbetar med Adobe Analytics- och Adobe Target-data finns i [exempelfrågereferensen][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
