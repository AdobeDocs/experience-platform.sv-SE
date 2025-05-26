---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Användargränssnittshandbok för frågetjänst
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare samt få åtkomst till frågor som har sparats av användare i organisationen.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 0553b8bc62d54c3ab98c60b16840ce730d9ed5c0
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 0%

---

# Användargränssnittshandbok för frågetjänst

Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare samt få åtkomst till frågor som har sparats av användare i organisationen. Om du vill komma åt användargränssnittet i [Adobe Experience Platform](https://platform.adobe.com) väljer du **[!UICONTROL Queries]** i den vänstra navigeringen. [!UICONTROL Queries] [!UICONTROL Overview] visas.

![Arbetsytan för frågetjänsten med frågor och fliken Översikt markerad.](../images/ui/overview/queries-overview.png)

## Översikt {#overview}

Fliken [!UICONTROL Overview] innehåller en smidig startpunkt för arbete med frågor och Distiller-mallar för data. Här har ni tillgång till alla funktioner som behövs för att skriva frågor, utforska datauppsättningar och analysera målgruppsdata, för att säkerställa ett smidigt arbetsflöde för dataanalys och målgruppsinsikter. Använd den här översikten för att lära dig vad du kan uppnå med Data Distiller och identifiera viktiga mätvärden för användningen av frågetjänsten.

### Huvudpaneler {#main-panels}

Sidan [!UICONTROL Overview] innehåller flera huvudavsnitt som hjälper dig att komma igång:

1. Välj **[!UICONTROL Create query]** om du snabbt vill navigera till frågeredigeraren för att skriva och köra nya frågor.
2. Välj **[!UICONTROL Learn more]** om du vill visa detaljerad dokumentation om hur du **[!UICONTROL Write queries]** ska användas.
3. Välj **[!UICONTROL Get started]** i avsnittet **[!UICONTROL Discover Data Distiller]** om du vill öppna översikten över Data Distiller och lära dig mer om tillgängliga funktioner.

![Arbetsytan för frågetjänsten med Skapa fråga, Läs mer och Kom igång är markerad.](../images/ui/overview/main-panels.png)

### Data Distiller-funktioner {#data-distiller-capabilities}

Avsnittet [!UICONTROL Data Distiller capabilities] innehåller dokumentationslänkar till mer avancerade data-Distiller-funktioner:

- **[[!UICONTROL Data exploration]](../use-cases/data-exploration.md)**: Lär dig hur du utforskar, felsöker och verifierar batchimporterade data med SQL.
- **[[!UICONTROL Derived datasets for Experience Platform applications]](../data-distiller/derived-datasets/overview.md)**: Lär dig hur du skapar härledda datauppsättningar som har stöd för komplexa och varierade användningsfall som maximerar ditt dataverktyg.
- **[[!UICONTROL AI/ML pipelines]](../data-distiller/ml-feature-pipelines/overview.md)**: Lär dig mer om viktiga koncept bakom de maskininlärningsverktyg du föredrar och hur du skapar anpassade modeller som stöder dina användningsfall för marknadsföring. Denna serie med guider beskriver de steg som krävs för att bygga rörledningar som förbereder data från Experience Platform för att mata anpassade modeller i maskininlärningsmiljön.
- **[[!UICONTROL SQL insights]](../data-distiller/sql-insights/overview.md)**: Lär dig mer om de viktigaste funktionerna och de steg som krävs för att utveckla en instrumentpanel för insikter från SQL med Data Distiller.

![Arbetsytan för frågetjänsten med Data Distiller-funktionsavsnittet markerat.](../images/ui/overview/data-distiller-capabilities.png)

### Rekommenderade Distiller-acceleratorer för data {#recommended-accelerators}

Välj en snabblänk för att navigera till relevanta Distiller-instrumentpaneler [!UICONTROL Templates]. Varje accelerator har kraftfulla verktyg och visualiseringar som hjälper er att analysera målgruppsdata, optimera segmenteringen och förbättra strategier för målinriktning.

- **[[!UICONTROL Advanced audience overlaps]](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)**: Från den här instrumentpanelen kan du analysera målgruppssnitt mellan flera målgruppssegment för att identifiera värdefulla insikter och optimera segmenteringsstrategier. Ni kan också exportera era insikter för vidare offlineanalys eller rapportering.
- **[[!UICONTROL Audience comparison]](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)**: Från den här instrumentpanelen kan du jämföra och kontrastera nyckeltal sida vid sida för att analysera två målgrupper i detalj. Dessa insikter hjälper er att förstå målgruppens storlek, tillväxt och andra viktiga resultatindikatorer, så att ni kan förfina segmenteringen och optimera målgruppsstrategier med datadrivna beslut.
- **[[!UICONTROL Audience trends]](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)**: Använd kontrollpanelen [!UICONTROL Audience trends] för att visualisera hur era målgrupper utvecklas över tid genom nyckelmått som målgruppstillväxt, identitetsantal och enskilda identitetsprofiler. Spåra trender för att hitta värdefulla insikter om målgruppernas beteende, så att ni kan förfina segmenteringen, öka engagemanget och optimera målgruppsstrategier för mer effektiva kampanjer.
Spåra målgruppsmått över tid för att övervaka förändringar i målgruppsstorlek, identitetstillväxt och övergripande engagemang.
- **[[!UICONTROL Audience identity overlaps]](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)**: Använd kontrollpanelen Överlappning av publikidentitet för att analysera identitetsöverlappningar inom valda målgrupper. Visualiseringar och tabelldata ger insikter för att optimera identitetssammanfogning, minska redundansen och förbättra segmenteringen. Dessa insikter möjliggör effektivare målgruppsanpassning, förbättrad personalisering och smidigare kundinteraktioner.

![Arbetsytan för frågetjänsten med Data Distiller-acceleratoravsnittet markerat.](../images/ui/overview/data-distiller-accelerators.png)

### Data Distiller-exempel {#data-distiller-examples}

Välj ett kort för att öppna dokumentationsguider och exempel som hjälper dig att få ut det mesta av Data Distiller:

- **[[!UICONTROL Decile-based derived datasets]](../use-cases/deciles-use-case.md)**: Lär dig hur du skapar dekorbaserade härledda datauppsättningar för segmentering och målgruppsskapande i Adobe Experience Platform. Med hjälp av ett lojalitetsscenario för flygbolag omfattar det schemadesign, decimalberäkningar och frågeexempel för rankning och sammanställning av data.
- **[[!UICONTROL Customer lifetime value]](../use-cases/customer-lifetime-value.md)**: Lär dig att spåra och visualisera kundlivstidsvärde med Real-Time CDP och anpassade instrumentpaneler. Använd dessa insikter för att utveckla strategier för att förvärva nya kunder, behålla befintliga kunder och maximera vinstmarginalerna.
- **[[!UICONTROL Propensity score]](../use-cases/propensity-score.md)**: Lär dig hur du fastställer benägenhetspoäng med hjälp av maskininlärningsmodeller. Den här guiden beskriver hur du skickar data för utbildning, tillämpar utbildade modeller med SQL och förutser sannolikheten för kundinköp.
- **[[!UICONTROL Consent analysis]](../../dashboards/insights-use-cases/consent-analysis.md)**: Lär dig hur du analyserar och spårar kundens samtycke med Real-Time CDP, Query Service och Data Distiller. Den här guiden beskriver hur du bygger upp kontrollpaneler för samtycke, finjusterar segmentering, håller koll på trender och ser till att de följs, vilket hjälper dig att skapa förtroende och leverera personaliserade upplevelser.
- **[[!UICONTROL Fuzzy match]](../use-cases/fuzzy-match.md)**: Lär dig hur du utför en &#39;luddig&#39; matchning på dina Experience Platform-data för att hitta ungefärliga matchningar och analysera strängens likhet mellan datauppsättningar. Följ den här guiden för att spara tid och göra dina data mer tillgängliga. Exemplet visar hur man kan matcha hotellrumsattribut mellan två data från resebyråer, och visa hur man effektivt kan matcha, jämföra och stämma av stora, komplexa datauppsättningar för att få en konsekvent och korrekt hantering.

![Arbetsytan för frågetjänsten med exempelavsnittet Data Distiller är markerat.](../images/ui/overview/data-distiller-examples.png)

### Nyckeltal {#key-metrics}

I avsnittet med nyckelmätvärden visas visualiseringar av viktiga data som hjälper dig att övervaka användningen av frågetjänsten. För varje diagram kan du markera ellipsen (`...`) i det övre högra hörnet följt av [!UICONTROL View more] om du vill visa ett tabellformat för resultaten eller hämta data som en CSV-fil om du vill visa dem i ett kalkylblad. Mer information finns i [Visa mer guide](../../dashboards/sql-insights-query-pro-mode/view-more.md).

#### Ange ett datumfilter {#set-date-filter}

Om du vill använda ett globalt datumfilter för dessa visualiseringar väljer du filterikonen (![En filterikon.](../../images/icons/filter-icon-white.png)) och justera datumintervallet i dialogrutan **[!UICONTROL Filters]**. Använd det här filtret om du vill anpassa de visade mätvärdena för en viss tidsram och göra analysen mer relevant.

![Dialogrutan Filter för nyckelmätningsdiagram i Query Service Workspace.](../images/ui/overview/filters-dialog.png)

#### [!UICONTROL Distiller batch queries] {#distiller-batch-queries}

Diagrammet [!UICONTROL Distiller batch queries] innehåller en beskrivning av frågeaktivitet per dag, som visar antalet bearbetade CTAS- och ITAS-frågor (interaktiva och schemalagda). Diagrammet markerar mönster, t.ex. taggar i interaktiva frågor på vissa dagar och sällan använda schemalagda frågor. Använd dessa insikter för att optimera prestanda genom att identifiera toppaktivitetsperioder, förfina schemaläggningsstrategier och balansera frågekörning för att förbättra arbetsflödets effektivitet och resursutnyttjande.

![Distiller batchfrågediagram.](../images/ui/overview/distiller-batch-queries.png)

#### [!UICONTROL Compute hours consumed] {#compute-hours-consumed}

Diagrammet [!UICONTROL Compute hours consumed] innehåller en daglig visualisering av beräkningstimmar som används för att bearbeta åtgärder i frågetjänsten. Använd dessa timtrender för att övervaka resursförbrukningen, identifiera perioder med hög efterfrågan och optimera frågekörningen för att säkerställa effektiv resursallokering och prestanda.

![Diagram över förbrukade beräkningstimmar.](../images/ui/overview/compute-hours-consumed.png)

#### [!UICONTROL Data exploratory queries]

Diagrammet [!UICONTROL Data exploratory queries] visar antalet SELECT-frågor som bearbetats på begäran varje dag. Den här visualiseringen visar aktivitetstrender för frågor, t.ex. ökning av användningen på vissa dagar, så att du lättare kan förstå när datautforskandet är som mest aktivt. Använd dessa insikter för att övervaka användningsmönster för frågor, balansera arbetsbelastningar och optimera resursallokeringen för analyser av data. Denna analys säkerställer en effektivare användning av frågetjänsten och förbättrad planering av perioder med hög efterfrågan.

![Diagrammet för dataundersökande frågor.](../images/ui/overview/data-exploratory-queries.png)

## Frågeredigeraren

Använd Frågeredigeraren för att skriva och köra frågor utan att använda en extern klient. Välj **[!UICONTROL Create Query]** om du vill öppna frågeredigeraren och skapa en ny fråga. Du kan även komma åt frågeredigeraren genom att välja en fråga på flikarna **[!UICONTROL Log]** eller **[!UICONTROL Templates]**. Om du väljer en fråga som har körts eller sparats tidigare, öppnas Frågeredigeraren och SQL:en för den valda frågan visas.

![Kontrollpanelen Frågor med Skapa fråga markerad.](../images/ui/overview/overview-create-query.png)

När du skriver i frågeredigeraren fyller redigeraren automatiskt i SQL-reserverade ord, tabeller och fältnamn i tabeller. När du är klar med frågan väljer du uppspelningsikonen (![Ikonen.](../../images/icons/play.png)) för att köra frågan. Fliken **[!UICONTROL Console]** nedanför redigeraren visar vad frågetjänsten gör för tillfället och anger när en fråga har returnerats. Fliken **[!UICONTROL Result]**, bredvid [!UICONTROL Console], visar frågeresultaten. Mer information om hur du använder Frågeredigeraren finns i [Frågeredigeringsguiden](./user-guide.md).

![Arbetsytan i frågeredigeraren.](../images/ui/overview/query-editor.png)

### Fliken Resultat {#results-tab}

Fliken [!UICONTROL Result] visar frågans tabellutdata efter körning. Använd den här fliken för att granska resultat, validera utdata och utföra uppföljningsåtgärder direkt i gränssnittet. I den här vyn kan du:

- Hämta resultat i CSV-, XLSX- eller JSON-format för offlineanalys. Se [Hämta frågeresultat](./user-guide.md#download-query-results).
- Visa resultatet i helskärmsläge för att granska stora tabeller eller breda datauppsättningar i en stödrasterlayout som kan storleksändras. Se [Visa resultat i helskärmsläge](./user-guide.md#view-results).
- Kopiera resultat till Urklipp i CSV-format för snabb inklistring i kalkylprogram. Se [Kopiera resultat](./user-guide.md#copy-results).

De här funktionerna är utformade för att stödja smidiga arbetsflöden för datavalidering, rapportering och delning - utan att behöva lämna Frågeredigeraren.

### Parametriserade frågor {#parameterized-queries}

Frågeredigeraren har stöd för parametriserade frågor, som gör att du kan infoga variabler i SQL-satser och dynamiskt tilldela värden vid körning. Den här funktionen förenklar återanvändbara frågor och ger större flexibilitet i arbetsflöden.

Du kan definiera parametrar när du skriver frågor och sedan tilldela värden via fliken [!UICONTROL Query parameters] innan du kör dem. Parameteriserade frågor är särskilt användbara för schemalagda frågor eller frågemallar som delas i hela organisationen.

Mer information om hur du definierar och använder parametrar finns i [Parametriserade frågor i Frågeredigeraren](./parameterized-queries.md).

## Schemalagda frågor {#scheduled-queries}

Frågor som redan har sparats som en mall kan schemaläggas för att köras med en vanlig stängsel. När du schemalägger en fråga kan du välja körningsfrekvens, start- och slutdatum, veckodag som den schemalagda frågan körs samt vilken datamängd som frågan ska exporteras till. Frågescheman ställs in med Frågeredigeraren.

Mer information om hur du schemalägger en fråga via användargränssnittet finns i [guiden om schemalagda frågor](./user-guide.md#scheduled-queries). Om du vill lära dig hur du lägger till scheman med API:t läser du [slutpunktshandboken för schemalagda frågor](../api/scheduled-queries.md).

När en fråga har schemalagts visas den i listan med schemalagda frågor på fliken [!UICONTROL Scheduled Queries]. Du hittar fullständig information om frågan, körningar, skapare och tidsinställningar genom att välja en schemalagd fråga i listan.

![Arbetsytan Frågor med fliken Schemalagda frågor är markerad och visar rader med frågescheman.](../images/ui/overview/scheduled-queries.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Namnfältet är antingen mallnamnet eller de första tecknen i SQL-frågan. Alla frågor som skapas via gränssnittet med Frågeredigeraren får i början ett namn. Om frågan skapades med API:t är namnet på frågan ett fragment av det SQL-uttryck som användes för att skapa frågan. |
| **[!UICONTROL Template]** | Frågans mallnamn. Välj ett mallnamn för att gå till Frågeredigeraren. Frågemallen visas i Frågeredigeraren. Om det inte finns något mallnamn markeras raden med ett bindestreck och det går inte att omdirigera till Frågeredigeraren för att visa frågan. |
| **[!UICONTROL SQL]** | Ett fragment av SQL-frågan. |
| **[!UICONTROL Run frequency]** | Den här kolumnen anger vid vilken tidpunkt frågan ska köras. De tillgängliga värdena är `Run once` och `Scheduled`. Frågor kan filtreras utifrån deras körningsfrekvens. |
| **[!UICONTROL Created by]** | Namnet på den användare som skapade frågan. |
| **[!UICONTROL Created]** | Tidsstämpeln när frågan skapades, i UTC-format. |
| **[!UICONTROL Last run timestamp]** | Den senaste tidsstämpeln när frågan kördes. Den här kolumnen visar om en fråga har körts enligt det aktuella schemat. |
| **[!UICONTROL Last run status]** | Status för den senaste frågekörningen. De tre statusvärdena är: `successful` `failed` eller `in progress`. |

Mer information om hur du [övervakar frågor via användargränssnittet för frågetjänsten](./monitor-queries.md) finns i dokumentationen.

## Mallar {#browse}

På fliken **[!UICONTROL Templates]** visas frågor som sparats av användare i din organisation. Det är praktiskt att tänka på dessa som frågeprojekt, eftersom frågor som sparas här fortfarande kan vara under uppbyggnad. Frågor som visas på fliken **[!UICONTROL Templates]** visas också som körningsfrågor på fliken **[!UICONTROL Log]** om de tidigare har körts av Query Service.

![En zoomad vy av fliken Mallar på kontrollpanelen för frågor som visar flera sparade frågor.](../images/ui/overview/templates.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Namnfältet är antingen frågenamnet som skapats av användaren eller de första tecknen i SQL-frågan. Alla frågor som skapas via gränssnittet med Frågeredigeraren får i början ett namn. Om frågan skapades via API är namnet på frågan ett fragment av det SQL-uttryck som användes för att skapa frågan. Du kan välja frågenamnet för att öppna frågan i Frågeredigeraren. Du kan också använda sökfältet för att söka efter [!UICONTROL Name] i en fråga. Sökningar är skiftlägeskänsliga. |
| **[!UICONTROL SQL]** | De första tecknen i SQL-frågan. Om du placerar pekaren över koden visas hela frågan. |
| **[!UICONTROL Modified by]** | Den sista användaren som ändrade frågan. Alla användare i organisationen som har tillgång till frågetjänsten kan ändra frågor. |
| **[!UICONTROL Last modified]** | Datum och tid för den senaste ändringen av frågan, i webbläsarens tidszon. |

Mer information om mallar i användargränssnittet för Experience Platform finns i dokumentationen för [frågemallar](./query-templates.md).

## Logg {#log}

Fliken **[!UICONTROL Log]** innehåller en lista med frågor som tidigare har körts. Som standard listas frågorna i loggen i omvänd kronologi.

![En zoomad vy av fliken Logg på kontrollpanelen för frågor som visar en lista med frågor i omvänd kronologisk ordning.](../images/ui/overview/log.png)

| Kolumn | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Frågenamnet som består av de första tecknen i SQL-frågan. Välj mallnamnet för att öppna vyn [!UICONTROL Query log details] för den körningen. Du kan använda sökfältet för att söka efter namnet på en fråga. Sökningar är skiftlägeskänsliga. |
| **[!UICONTROL Start time]** | Tiden då frågan kördes. |
| **[!UICONTROL Complete time]** | Den tidpunkt då frågan kördes. |
| **[!UICONTROL Status]** | Frågans aktuella status. |
| **[!UICONTROL Dataset]** | Den indatamängd som används av frågan. Välj den datauppsättning som du vill gå till informationsskärmen för indatauppsättningar. |
| **[!UICONTROL Client]** | Klienten som används för frågan. |
| **[!UICONTROL Created by]** | Namnet på den person som skapade frågan. |

>[!NOTE]
>
>Välj pennikonen (![En pennikon.](/help/images/icons/edit.png)) från valfri rad i frågeloggen för att navigera till frågeredigeraren. Frågan är ifylld i förväg för smidig redigering.

Mer information om loggfilerna som genereras automatiskt av en frågetaghändelse finns i [frågeloggsdokumentationen](./query-logs.md).

## Referenser

Fliken **[!UICONTROL Credentials]** visar både dina utgångsdatum och ej utgångsdatum. Mer information om hur du använder dessa autentiseringsuppgifter för att ansluta till externa klienter finns i [handboken för autentiseringsuppgifter](../clients/overview.md).

![Kontrollpanelen Frågor med fliken Autentiseringsuppgifter markerad.](../images/ui/overview/credentials.png)

## Nästa steg

Nu när du är bekant med användargränssnittet för frågetjänsten på [!DNL Experience Platform] kan du komma åt Frågeredigeraren och börja skapa egna frågeprojekt som du kan dela med andra användare i organisationen. Mer information om hur du redigerar och kör frågor i Frågeredigeraren finns i [Användarhandboken för Frågeredigeraren](./user-guide.md).
