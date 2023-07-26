---
keywords: Experience Platform;home;populära topics;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Användargränssnittshandbok för frågeredigeraren
description: Frågeredigeraren är ett interaktivt verktyg som tillhandahålls av Adobe Experience Platform Query Service, som gör att du kan skriva, validera och köra frågor för kundupplevelsedata i användargränssnittet i Experience Platform. Frågeredigeraren har stöd för att utveckla frågor för analys och datautforskande, och gör att du kan köra interaktiva frågor i utvecklingssyfte samt icke-interaktiva frågor för att fylla i datauppsättningar i Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: e30942aec6c66aeed8375d6221b454725f5a958d
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 0%

---

# [!DNL Query Editor] Användargränssnittsguide

[!DNL Query Editor] är ett interaktivt verktyg från Adobe Experience Platform [!DNL Query Service]som gör det möjligt att skriva, validera och köra frågor om kundupplevelsedata i [!DNL Experience Platform] användargränssnitt. [!DNL Query Editor] har stöd för utveckling av frågor för analys och datautforskande och gör att du kan köra interaktiva frågor i utvecklingssyfte samt icke-interaktiva frågor för att fylla i datauppsättningar i [!DNL Experience Platform].

Mer information om begrepp och funktioner i [!DNL Query Service], se [Översikt över frågetjänsten](../home.md). Mer information om hur du navigerar i användargränssnittet för frågetjänsten på [!DNL Platform], se [Översikt över användargränssnittet i frågetjänsten](./overview.md).

## Komma igång {#getting-started}

[!DNL Query Editor] erbjuder flexibel körning av frågor genom att ansluta till [!DNL Query Service]och frågor körs bara när den här anslutningen är aktiv.

### Ansluter till [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] tar några sekunder att initiera och ansluta till [!DNL Query Service] när den öppnas. Konsolen talar om för dig när den är ansluten, vilket visas nedan. Om du försöker köra en fråga innan redigeraren har anslutit, fördröjs körningen tills anslutningen är klar.

![Frågeredigerarens konsolutdata vid den första anslutningen.](../images/ui/query-editor/connect.png)

### Hur frågor körs från [!DNL Query Editor] {#run-a-query}

Frågor som körs från [!DNL Query Editor] köra interaktivt vilket innebär att om du stänger webbläsaren eller navigerar bort så avbryts frågan. Detsamma gäller för frågor som skapas för att generera datauppsättningar från frågeutdata.

## Frågeredigering med [!DNL Query Editor] {#query-authoring}

Använda [!DNL Query Editor]kan du skriva, köra och spara frågor om kundupplevelsedata. Alla frågor har körts eller sparats i [!DNL Query Editor] är tillgängliga för alla användare i organisationen med tillgång till [!DNL Query Service].

### Komma åt [!DNL Query Editor] {#accessing-query-editor}

I [!DNL Experience Platform] Gränssnitt, välj **[!UICONTROL Queries]** i den vänstra navigeringsmenyn för att öppna [!DNL Query Service] arbetsyta. För att börja skriva frågor väljer du **[!UICONTROL Create Query]** längst upp till höger på skärmen. Den här länken är tillgänglig från någon av sidorna i [!DNL Query Service] arbetsyta.

![Översiktsfliken i arbetsytan Frågor med frågan Skapa markerad.](../images/ui/query-editor/create-query.png)

### Förbättrad frågeredigerare {#enhanced-editor-toggle}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_enhancedEditorToggle"
>title="Förbättrad redigeringsfunktion"
>abstract="Växla mellan den äldre och förbättrade versionen av Frågeredigeraren. Den äldre versionen är aktiverad som standard, men den förbättrade versionen har bättre tillgänglighet och stöd för flera teman. Mer information om dessa ändringar finns i dokumentationen."

Med ett användargränssnitt kan du växla mellan den tidigare och förbättrade versionen av Frågeredigeraren. Den äldre versionen är aktiverad som standard, men den förbättrade versionen har bättre tillgänglighet och stöd för flera teman. Aktivera den förbättrade versionen för att komma åt inställningarna för Frågeredigeraren.

![Frågeredigeraren med den förbättrade frågeredigeraren markerad.](../images/ui/query-editor/enhanced-query-editor-toggle.png)

När du aktiverar växlingsknappen ändras redigeraren till ett ljust tema och syntaxens läsbarhet förbättras. En inställningsikon visas också ovanför inmatningsfältet i Frågeredigeraren, som innehåller det automatiska avslutningsreglaget. Från inställningsikonen kan du aktivera mörkt tema eller inaktivera/aktivera automatisk komplettering.

>[!TIP]
>
>Med den förbättrade frågeredigeraren kan du [!UICONTROL Disable syntax auto complete] när du redigerar en fråga utan att förlora förloppet. Om du inaktiverar funktionen för automatisk komplettering när du redigerar försvinner vanligtvis alla ändringar i frågan.

Om du vill aktivera mörka eller ljusa teman väljer du inställningsikonen (![En inställningsikon.](../images/ui/query-editor/settings-icon.png)) följt av alternativet i listrutan som visas.

![Frågeredigeraren med inställningsikonen och alternativet Aktivera mörkt tema på den nedrullningsbara menyn markerat.](../images/ui/query-editor/query-editor-settings.png)

### Skriver frågor {#writing-queries}

[!UICONTROL Query Editor] är organiserat för att göra det så enkelt att skriva frågor som möjligt. Skärmbilden nedan visar hur redigeraren visas i användargränssnittet, med SQL-postfältet och **Spela upp** markerad.

![Frågeredigeraren med SQL-indatafältet och uppspelning markerat.](../images/ui/query-editor/editor.png)

För att minimera utvecklingstiden rekommenderar vi att du utvecklar dina frågor med begränsningar för antalet rader som returneras. Exempel, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. När du har verifierat att frågan ger det förväntade resultatet tar du bort gränserna och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata.

### Skrivverktyg i [!DNL Query Editor] {#writing-tools}

- **Automatisk syntaxmarkering:** Gör det enklare att läsa och ordna SQL.

![En SQL-sats i Frågeredigeraren som visar färgmarkering för syntaxen.](../images/ui/query-editor/syntax-highlight.png)

- **SQL-nyckelord har slutförts automatiskt:** Börja skriva frågan, använd sedan piltangenterna för att navigera till önskad term och trycka på **Retur**.

![Några tecken i SQL med listrutan Komplettera automatiskt som innehåller alternativ från Frågeredigeraren.](../images/ui/query-editor/syntax-auto.png)

- **Tabell och fält har fyllts i automatiskt:** Börja skriva det tabellnamn som du vill använda `SELECT` navigera sedan till tabellen du letar efter med piltangenterna och tryck på **Retur**. När en tabell har markerats identifieras fält i den tabellen automatiskt.

![Indata från Frågeredigeraren med förslag på listtabellnamn.](../images/ui/query-editor/tables-auto.png)

### Växla mellan automatisk komplettering av användargränssnittskonfigurationen {#auto-complete}

The [!DNL Query Editor] föreslår automatiskt potentiella SQL-nyckelord tillsammans med tabell- eller kolumninformation för frågan när du skriver den. Funktionen för automatisk komplettering är aktiverad som standard och kan när som helst inaktiveras eller aktiveras genom att du väljer [!UICONTROL Syntax auto-complete] till höger i Frågeredigeraren.

Konfigurationsinställningen som slutförs automatiskt är per användare och sparas för den användarens efterföljande inloggningar.

![Frågeredigeraren med syntaxen auto-complete aktiverad.](../images/ui/query-editor/auto-complete-toggle.png)

Om du inaktiverar den här funktionen hindras flera metadatakommandon från att bearbetas och ger rekommendationer som vanligtvis underlättar för författaren när han/hon redigerar frågor.

När du använder växlingsknappen för att aktivera funktionen för automatisk komplettering blir förslag på tabell- och kolumnnamn samt SQL-nyckelord tillgängliga efter en kort paus. Ett meddelande om att åtgärden lyckades i konsolen under Frågeredigeraren anger att funktionen är aktiv.

Om du inaktiverar funktionen för automatisk komplettering måste du uppdatera sidan för att funktionen ska börja gälla. En bekräftelsedialogruta med tre alternativ visas när du inaktiverar [!UICONTROL Syntax auto-complete] växla:

- [!UICONTROL Cancel]
- [!UICONTROL Save changes and refresh]
- [!UICONTROL Refresh without saving changes]

>[!IMPORTANT]
>
>Om du skriver eller redigerar en fråga när du inaktiverar den här funktionen måste du spara alla ändringar i frågan innan du uppdaterar sidan, annars går alla förlopp förlorade.

![Bekräftelsedialogrutan för att inaktivera funktionen för automatisk komplettering.](../images/ui/query-editor/confirmation-dialog.png)

Om du vill inaktivera funktionen för automatisk komplettering väljer du lämpligt bekräftelsealternativ.

### Felidentifiering {#error-detection}

[!DNL Query Editor] validerar automatiskt en fråga medan du skriver den, vilket ger generisk SQL-validering och specifik körningsvalidering. Om en röd understrykning visas under frågan (som bilden nedan visar) representerar den ett fel i frågan.

![Indata från Frågeredigeraren som visar SQL understruket i rött för att indikera ett fel.](../images/ui/query-editor/syntax-error-highlight.png)

När fel upptäcks kan du visa de specifika felmeddelandena genom att hovra över SQL-koden.

![En dialogruta med ett felmeddelande.](../images/ui/query-editor/linting-error.png)

### Frågeinformation {#query-details}

Om du vill visa en fråga i Frågeredigeraren väljer du en sparad mall i dialogrutan [!UICONTROL Templates] -fliken. Panelen Frågeinformation innehåller mer information och verktyg för att hantera den valda frågan.

![Frågeredigeraren med frågeinformationspanelen markerad.](../images/ui/query-editor/query-details.png)

På den här panelen kan du generera en utdatamängd direkt från användargränssnittet, ta bort eller namnge den visade frågan och lägga till ett schema i frågan.

På den här panelen visas även användbara metadata som den senaste gången frågan ändrades och vem som ändrade den, om tillämpligt. Om du vill generera en datauppsättning väljer du **[!UICONTROL Output Dataset]**. The **[!UICONTROL Output Dataset]** visas. Ange ett namn och en beskrivning och välj **[!UICONTROL Run Query]**. Den nya datauppsättningen visas i **[!UICONTROL Datasets]** på [!DNL Query Service] användargränssnitt på [!DNL Platform].

### Schemalagda frågor {#scheduled-queries}

Frågor som har sparats som en mall kan schemaläggas från Frågeredigeraren. Med schemaläggningsfrågor kan du automatisera frågekörningar på en anpassad cache. Du kan schemalägga frågor baserat på frekvens, datum och tid och även välja en utdatamängd för dina resultat om det behövs. Frågescheman kan även inaktiveras eller tas bort via användargränssnittet.

Scheman ställs in i Frågeredigeraren. När du använder Frågeredigeraren kan du bara lägga till ett schema i en fråga som redan har skapats, sparats och körts. Samma begränsning gäller inte för [!DNL Query Service] API:

Läs dokumentationen om frågescheman för att lära dig mer om [skapa frågescheman i användargränssnittet](./query-schedules.md). Du kan även läsa mer om hur du lägger till scheman med API:t i [slutpunktsguide för schemalagda frågor](../api/scheduled-queries.md).

Alla schemalagda frågor läggs till i listan i [!UICONTROL Scheduled queries] -fliken. Från den arbetsytan kan du övervaka statusen för alla schemalagda frågejobb via gränssnittet. På [!UICONTROL Scheduled queries] kan du hitta viktig information om frågekörningar och prenumerera på aviseringar. Den tillgängliga informationen omfattar status, schemainformation och felmeddelanden/koder om en körning misslyckas. Se [Övervaka dokument för schemalagda frågor](./monitor-queries.md) för mer information.

### Sparar frågor {#saving-queries}

The [!DNL Query Editor] innehåller en funktion för att spara som gör att du kan spara en fråga och arbeta med den senare. Om du vill spara en fråga väljer du **[!UICONTROL Save]** i det övre högra hörnet av [!DNL Query Editor]. Innan en fråga kan sparas måste ett namn anges för frågan med hjälp av **[!UICONTROL Query Details]** -panelen.

>[!NOTE]
>
>Frågor som namngivits och sparats i med Frågeredigeraren är tillgängliga som mallar på kontrollpanelen Fråga [!UICONTROL Templates] -fliken. Se [malldokumentation](./query-templates.md) för mer information.

### Söka efter tidigare frågor {#previous-queries}

Alla frågor som körs från [!DNL Query Editor] finns i loggtabellen. Du kan använda sökfunktionerna i **[!UICONTROL Log]** för att hitta frågekörningar. Sparade frågor listas i **[!UICONTROL Templates]** -fliken.

Om en fråga har schemalagts [!UICONTROL Scheduled Queries] -fliken ger förbättrad synlighet via användargränssnittet för dessa frågefunktioner. Se [frågeövervakningsdokumentation](./monitor-queries.md) för mer information.

>[!NOTE]
>
>Frågor som inte körs sparas inte av loggen. För att frågan ska vara tillgänglig i [!DNL Query Service]måste den köras eller sparas i [!DNL Query Editor].

## Köra frågor med Frågeredigeraren {#executing-queries}

Köra en fråga i [!DNL Query Editor]kan du ange SQL i redigeraren eller läsa in en tidigare fråga från **[!UICONTROL Log]** eller **[!UICONTROL Templates]** och markera **Spela upp**. Status för frågekörning visas i **[!UICONTROL Console]** nedan och utdata visas i **[!UICONTROL Results]** -fliken.

### Konsol {#console}

Konsolen ger information om status och funktion för [!DNL Query Service]. Konsolen visar anslutningsstatus för [!DNL Query Service], frågeåtgärder som körs och felmeddelanden som är ett resultat av dessa frågor.

![Fliken Konsol i frågeredigeringskonsolen.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>Konsolen visar bara fel som uppstått efter körningen av en fråga. Det visar inte de frågevalideringsfel som inträffar innan en fråga körs.

### Frågeresultat {#query-results}

När en fråga är klar visas resultatet i **[!UICONTROL Results]** -flik, bredvid **[!UICONTROL Console]** -fliken. I den här vyn visas frågans tabellutdata med upp till 100 rader. I den här vyn kan du verifiera att frågan ger förväntat resultat. Om du vill generera en datauppsättning med frågan tar du bort begränsningar för returnerade rader och kör frågan med `CREATE TABLE tablename AS SELECT` för att generera en datauppsättning med utdata. Se [skapa datauppsättningar, genomgång](./create-datasets.md) för instruktioner om hur du genererar en datauppsättning från frågeresultat i [!DNL Query Editor].

![Fliken Resultat i frågeredigeringskonsolen som visar resultatet av en frågekörning.](../images/ui/query-editor/query-results.png)

## Kör frågor med [!DNL Query Service] videokurs {#query-tutorial-video}

I följande video visas hur du kör frågor i Adobe Experience Platform-gränssnittet och i en PSQL-klient. I videon visas också hur du använder enskilda egenskaper i ett XDM-objekt, Adobe-definierade funktioner och hur du använder CREATE TABLE AS SELECT-frågor (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nästa steg

Nu när du vet vilka funktioner som är tillgängliga i [!DNL Query Editor] och hur du navigerar i programmet kan du börja skapa egna frågor direkt i [!DNL Platform]. Mer information om hur du kör SQL-frågor mot datauppsättningar i [!DNL Data Lake], se guiden på [köra frågor](../best-practices/writing-queries.md).
