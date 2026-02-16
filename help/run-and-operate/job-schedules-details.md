---
description: Lär dig hur du visar detaljerad information om datauppsättningar och enskilda jobbkörningar i Jobbscheman.
solution: Experience Platform
title: Visa information om jobbschema
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---


# Visa information om jobbschema

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] är för närvarande tillgängligt som en begränsad version och endast för följande Real-Time CDP-jobb:
>
> * Intag av batchdata i sjö
> * Inmatning av gruppprofil
> * Grupputleverans
> * Aktivering av batchmål.

När du felsöker jobbfel eller undersöker prestandaproblem behöver du detaljerad information om specifika datauppsättningar och deras jobb. Med gränssnittet [Jobbscheman](job-schedules.md) kan du gå nedåt från tidslinjevyn till enskilda datauppsättningar och jobb för att förstå körningshistorik, tidsinställning och status.

Använd den här detaljerade vyn för att:

* Undersök varför ett specifikt jobb misslyckades eller tog längre tid än förväntat
* Granska körningshistoriken för en datauppsättning över tiden
* Förstå timings- och tidsmönster för batchjobb
* Identifiera vilka specifika batchar som orsakar pipelineproblem
* Samla information som behövs för felsökning med Adobe Support

## Förhandskrav {#prerequisites}

Innan du visar jobbinformation bör du:

* Har åtkomst till [!UICONTROL Job Schedules] med behörigheterna **[!UICONTROL View Job Schedules]** och **[!UICONTROL View Profile Management]** [åtkomstkontroll](/help/access-control/home.md#permissions).
* Lär dig mer om gränssnittet [Jobbscheman](job-schedules.md#understanding-interface) och tidslinjevyn.
* Förstå de olika [jobbtyperna](job-schedules.md#job-schedules-details) (sjöintag, profilinmatning, segmentering, aktivering).

## Om informationshierarkin {#details-hierarchy}

Jobbscheman innehåller tre nivåer av detaljrikedom, så att du kan gå från breda mönster till specifika frågor:

| Visningsnivå | Vad det visar | När ska den användas |
|------------|---------------|----------------|
| **Tidslinjevy** | Alla datauppsättningar och deras schemalagda jobb under den valda tidsperioden | Identifiera mönster, hitta [antimönster](job-schedules-anti-patterns.md) och få en översikt över hela din pipeline |
| **Datauppsättningsinformation** | Sammanlagda mätvärden och körningshistorik för en enskild datauppsättning | Spåra övergripande prestanda för en datauppsättning, förstå datavolymer och granska jobbfrekvens |
| **Information om jobbkörning** | Specifik körningsinformation för en enskild jobbkörning | Undersöker varför ett visst jobb misslyckades, kontrollerar exakt timing och verifierar poster som bearbetats |

**Navigeringsflöde**: Börja med tidslinjevyn för att identifiera problem → Välj en datauppsättning för att se information → Välj en specifik jobbkörning för att undersöka detaljer.

### Förstå tidslinjevyn {#timeline-visualization}

I tidslinjevyn används en vågrät och lodrät layout som hjälper dig förstå jobbscheman och kritiska bearbetningstider:

* **Vågrät axel (tidsförlopp)**: Datauppsättningar och deras jobbkörningar visas på tidslinjen från vänster till höger, och visar när jobb körs under den valda tidsperioden (idag, igår eller senaste 7 dagar). Varje färgad stapel representerar en jobbkörning, placerad vågrätt enligt start- och sluttiden.

* **Lodrät axel (schemalagda starttider)**: Kritiska schemalagda starttider visas som lodräta linjer som sträcker sig över alla datauppsättningar, vilket gör det enkelt att se tidsförhållandet mellan uppströms-jobb och nedströmsbearbetning:
   * **Blå lodrät linje**: Representerar när segmentering är schemalagd att börja
   * **Svart lodrät linje**: Representerar när målaktiveringen är schemalagd att börja

Med den här layouten kan du snabbt identifiera tidsförhållanden mellan dina dataredriefunktioner och efterföljande bearbetning. I idealfallet bör jobb uppströms (som datasjön och profilintag) slutföras till vänster om dessa vertikala markörer, vilket säkerställer att data är klara innan segmentering och aktivering börjar. Jobb som sträcker sig utanför dessa markörer anger potentiella timingproblem där processer längre fram i kedjan kan börja innan data är helt förberedda.

### Vilken vy ska jag använda? {#which-view}

| Jag måste... | Använd den här vyn |
|--------------|---------------|
| Visa alla mina profilaktiverade datauppsättningar och deras scheman samtidigt | [Tidslinjevy](job-schedules.md) |
| Identifiera schemaläggningskonflikter eller mönster | [Tidslinjevy](job-schedules.md) |
| Spåra övergripande prestanda för en datauppsättning | [Datauppsättningsinformation](#view-dataset-details) |
| Se hur många totala poster en datauppsättning har bearbetat | [Datauppsättningsinformation](#view-dataset-details) |
| Jämför jobbprestanda över tid för en datauppsättning | [Datauppsättningsinformation](#view-dataset-details) |
| Undersök varför ett specifikt jobb misslyckades | [Information om jobbkörning](#view-job-details) |
| Kontrollera den exakta tidpunkten för en viss jobbkörning | [Information om jobbkörning](#view-job-details) |
| Verifiera poster som bearbetats i en enda körning | [Information om jobbkörning](#view-job-details) |
| Få detaljerade felmeddelanden | [Information om jobbkörning](#view-job-details) → Välj dataflödes-ID |

## Visa datauppsättningsinformation {#view-dataset-details}

Så här visar du information om en viss datauppsättning:

1. Leta reda på datauppsättningen som du vill undersöka i tidslinjevyn **[!UICONTROL Job Schedules]**.
2. Välj datauppsättningsnamnet i den vänstra kolumnen.

Vyn med datauppsättningsinformation öppnas på en panel till höger och visar information om alla jobb som är kopplade till den här datauppsättningen.

![Panelen med datauppsättningsinformation som visar aggregerade insjö- och profilanvändningsmått för en vald datauppsättning.](assets/job-schedules/view-dataset-details.png)

Panelen med datauppsättningsinformation visar datauppsättningsnamn, ID och jobbspecifika mått ordnade efter jobbtyp. Överst på panelen visas datauppsättnings-ID:t som en klickbar länk. Välj det här ID:t för att navigera till sidan med information om hela datauppsättningen.

Panelen med information om datauppsättningar innehåller följande mått:

### Mätvärden för sjöförtäring {#lake-ingestion-metrics}

För datauppsättningar med data Lake Input-jobb visar panelen följande mått:

| Mått | Beskrivning | Använd för |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Det totala antalet ifyllningsjobb för sjömatning som har slutförts för den här datauppsättningen | Aktivitetsspårning |
| **[!UICONTROL Runs in progress]** | Hur många sjömatningsjobb som körs för närvarande | Identifiering av flaskhalsar |
| **[!UICONTROL Total records added]** | Det sammanlagda antalet nya poster som lagts till i datasjön under alla jobbkörningar | Volymövervakning |
| **[!UICONTROL Total ingestion time]** | Den kombinerade varaktigheten för alla ingrepp i sjön av data | Utvärdering av bearbetningstid |
| **[!UICONTROL Total records updated]** | Det ackumulerade antalet befintliga poster som uppdaterades under importen | Uppdatera mönsteranalys |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | Genomsnittlig genomströmningsfrekvens för ingångsjobb i sjön | Prestandajämförelse |

### Profilätvärden {#profile-ingestion-metrics}

För datauppsättningar med profilinläsningsjobb visar panelen följande mått:

| Mått | Beskrivning | Använd för |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Det totala antalet profilinmatningsjobb som har slutförts för den här datauppsättningen | Aktivitetsspårning |
| **[!UICONTROL Runs in progress]** | Hur många profilbearbetningsjobb som körs för närvarande | Fördröjningsidentifiering |
| **[!UICONTROL Total profiles created]** | Det kumulativa antalet nya profiler som skapas från den här datauppsättningen för alla jobbkörningar | Profiltillväxtövervakning |
| **[!UICONTROL Total profile ingestion time]** | Den kombinerade varaktigheten för alla profilinmatningsjobb | Identifiering av timingutleverans |
| **[!UICONTROL Total profiles updated]** | Det kumulativa antalet befintliga profiler som uppdaterades med data från den här datauppsättningen | Uppdatera frekvensspårning |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | Genomsnittlig genomströmningsfrekvens för profilinmatningsjobb | Prestandaövervakning |

>[!NOTE]
>
> Dessa värden visar kumulativa summor för alla jobbkörningar för den här datamängden. Om du vill visa information om en viss körning väljer du ett jobb direkt på tidslinjen.

## Filtrera datauppsättningar på tidslinjen {#filter-datasets}

När du har många datauppsättningar med schemalagda jobb kanske du vill fokusera på specifika datauppsättningar i stället för att visa alla samtidigt. Med datauppsättningsfiltret kan du välja vilka datauppsättningar som ska visas i tidslinjevyn.

![På datauppsättningsfilterpanelen kan du välja vilka datauppsättningar som ska visas i tidslinjevyn.](assets/job-schedules/view-datasets.gif)

Så här filtrerar du de datauppsättningar som visas på tidslinjen:

1. Leta efter räknaren för datauppsättningar i det övre vänstra hörnet i tidslinjevyn (till exempel&quot;2 datauppsättningar&quot;).
2. Markera filterikonen bredvid datauppsättningsräknaren.
3. En panel för val av datauppsättning öppnas med alla tillgängliga profilaktiverade datauppsättningar med schemalagda jobb.
4. Markera eller avmarkera datauppsättningar om du vill visa eller dölja dem i tidslinjevyn.
5. Tidslinjen uppdateras omedelbart så att endast de markerade datauppsättningarna visas.

Använd filtrering för att:

* **Fokusera på specifika datakällor**: När du felsöker en viss dataredning kan du filtrera så att bara de relevanta datamängderna visas.
* **Minska den visuella skärpan**: Om du har många datauppsättningar kan du med filtrering se mönster tydligare för en delmängd av data.
* **Jämför relaterade datamängder**: Välj bara datamängder som är relaterade för att förstå deras schemaläggningsrelation.
* **Undersök mönster**: När du identifierar ett potentiellt [konfigurationsproblem](job-schedules-anti-patterns.md) kan du filtrera till de berörda datauppsättningarna för att undersöka dem närmare.

Filtret kvarstår under sessionen, så du kan navigera mellan tidsperioder (i dag, i går, i 7 dagar) samtidigt som du behåller datauppsättningsmarkeringen.

## Visa information om enskilda jobbkörningar {#view-job-details}

När du behöver undersöka en viss jobbkörning väljer du den på tidslinjen för att se detaljerad körningsinformation för den aktuella körningen.

### Information om jobbkörning {#access-job-details}

Så här visar du information för en viss jobbkörning:

1. Leta reda på den jobbkörning du vill undersöka i tidslinjevyn [!UICONTROL Job Schedules].
2. Välj jobbindikatorn på tidslinjen (det färgade fältet som representerar jobbet).

Panelen **[!UICONTROL Dataflow run details]** öppnas och visar information om den specifika jobbkörningen.

![Panelen med information om dataflödeskörning som visar körningsinformation för en specifik jobbkörning.](assets/job-schedules/job-details.png)

### Information om dataflödeskörning {#dataflow-run-details}

På informationsfältet för dataflödeskörning visas information om den specifika jobbkörningen, ordnade efter jobbtyp. När det gäller intag av vatten kommer du att se information om både sjöintag och intagande av profiler.

#### Information om ingressjobb i sjön {#lake-ingestion-job-details}

| Fält | Beskrivning |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Den unika identifieraren för den här specifika körningen av sjömatningsjobbet. Välj ID för att visa information om fullständig dataflödesövervakning. |
| **[!UICONTROL Run status]** | Resultatet av jobbet (Slutfört, Misslyckat, Pågår, Köat). En grön indikator visar att åtgärden har slutförts. |
| **[!UICONTROL Started at]** | Datum och tid då sjömatningsjobbet började utföras. |
| **[!UICONTROL Completed at]** | Datum och tid då sjömatningsjobbet slutfördes. |
| **[!UICONTROL Records added]** | Antalet nya poster som lagts till i datasjön under den här jobbkörningen. |
| **[!UICONTROL Records updated]** | Antalet befintliga poster som uppdaterades i datasjön under jobbkörningen. |

#### Information om jobb för profilinmatning {#profile-ingestion-job-details}

| Fält | Beskrivning |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Den unika identifieraren för den här specifika profilens ifyllningsjobb. Välj ID för att visa information om fullständig dataflödesövervakning. |
| **[!UICONTROL Run status]** | Resultatet av jobbet (Slutfört, Misslyckat, Pågår, Köat). En grön indikator visar att åtgärden har slutförts. |
| **[!UICONTROL Started at]** | Det datum och den tid då profilens ifyllningsjobb började köras. |
| **[!UICONTROL Completed at]** | Det datum och den tid då profilinmatningsjobbet slutförde körningen. |
| **[!UICONTROL Records added]** | Antalet nya profiler som skapas under jobbkörningen. |
| **[!UICONTROL Records updated]** | Antalet befintliga profiler som uppdaterades under jobbkörningen. |

### Om jobbkörningsflöde {#job-execution-flow}

När du tittar på ett specifikt jobb kan du se förhållandet mellan sjökonsumtion och intag av profiler:

* **Intrågningen i sjön körs först**: Data läses in i sjön och valideras.
* **Inmatning av profiler följer**: När sjömatningen är klar bearbetas giltiga poster i profilarkivet.
* **Tidsinställning har betydelse**: Observera tidsskillnaden mellan när sjömatning slutförs och när profilåtkomsten startar. Mellanrum här kan påverka processerna längre fram i kedjan, t.ex. segmentering.

**Använd jobbkörningsinformation för**:

* Verifiera att ett specifikt jobb har slutförts
* Beräkna den faktiska varaktigheten för en jobbkörning (slutförd tid minus starttid)
* Förstå hur många poster som har bearbetats i en viss körning
* Jämför prestanda för olika jobbkörningar
* Få detaljerad dataflödesövervakning för felsökningsfel
* Identifiera timingproblem mellan sjö- och profilintagsfaser

## Felsökning med jobbinformation {#troubleshooting}

Använd jobbinformation för att undersöka problem och bestämma nästa steg:

**Misslyckade jobb**: Välj ID för dataflödeskörning om du vill visa felinformation på kontrollpanelen. Kontrollera [datauppsättningsinformationen](#view-dataset-details) för återkommande mönster, se [tidslinjen](job-schedules.md) för resurskonflikter och identifiera [anti-patterns](job-schedules-anti-patterns.md) i konfigurationen.

**Långsamma jobb**: Jämför varaktighet med historiska genomsnitt i [datamängdsmått](#view-dataset-details). Vanliga orsaker är [schemaöverlappning](job-schedules-anti-patterns.md#schedule-overlap-pattern), [tät gruppstackning](job-schedules-anti-patterns.md#scheduled-density) eller ökad datavolym.

**Registreringsfel**: Jämför poster för sjöförtäring mot poster för profilförtäring i jobbkörningsinformationen. Inmatning av profiler visar vanligtvis färre poster på grund av identitetskrav och regler för datakvalitet.

Detaljerad information om dataflödets status finns i [Övervaka dataflöde för inhämtning av data från sjön](../dataflows/ui/monitor-sources.md), [Övervaka dataflöden för profiler](../dataflows/ui/monitor-profiles.md), [Övervaka dataflöden för målgrupper](../dataflows/ui/monitor-audiences.md) och [Övervaka dataflöden för mål](../dataflows/ui/monitor-destinations.md).

## Nästa steg {#next-steps}

Efter att du lärt dig hur du visar jobbinformation:

* Granska översikten över [Jobbscheman](job-schedules.md) för att förstå tidslinjevyn och gränssnittet.
* Lär dig mer om [antimönster](job-schedules-anti-patterns.md) för att förhindra vanliga konfigurationsproblem.
* Förstå [gruppinläsning](../ingestion/batch-ingestion/overview.md) för att optimera dina scheman för datainläsning.
* Utforska [övervakning av måldataflöden](../dataflows/ui/monitor-destinations.md) för att se om pipeline är synlig från början till slut.
