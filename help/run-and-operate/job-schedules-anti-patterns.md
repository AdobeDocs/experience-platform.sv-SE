---
description: Lär dig hur du identifierar och åtgärdar vanliga mönster för skydd mot jobbscheman i Adobe Experience Platform.
solution: Experience Platform
title: Identifiera kantmönster i jobbschemat
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---


# Identifiera kantmönster för jobbschema

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] är för närvarande tillgängligt som en begränsad version och endast för följande Real-Time CDP-jobb:
>
> * Intag av batchdata i sjö
> * Inmatning av gruppprofil
> * Grupputleverans
> * Aktivering av batchmål.

Tidslinjevyn [Jobbscheman](job-schedules.md) hjälper dig att identifiera vanliga konfigurationsproblem som kan påverka dataredningens prestanda och tillförlitlighet negativt. Dessa antimönster leder ofta till jobbfel, inkonsekvenser i data eller försämrade systemprestanda. Genom att hitta dessa mönster tidigt kan du konfigurera om dina jobb för att undvika problem innan de påverkar din verksamhet.

## Förhandskrav {#prerequisites}

Innan du identifierar antimönster bör du:

* Har åtkomst till [!UICONTROL Job Schedules] med behörigheten **[!UICONTROL View Job Schedules]** [åtkomstkontroll](/help/access-control/home.md#permissions).
* Lär dig mer om gränssnittet [Jobbscheman](job-schedules.md#understanding-interface) och hur du läser tidslinjevyn.
* Förstå grundläggande [gruppinmatning](../ingestion/batch-ingestion/overview.md), [segmentering](../segmentation/home.md) och [profilbearbetning](../profile/home.md).

## Snabbreferens {#anti-pattern-quick-reference}

| Kantmönster | Vad du ser på tidslinjen | Primär påverkan | Allvarlighetsgrad |
|--------------|----------------------------------|----------------|----------|
| [Schemaöverlappning](#schedule-overlap-pattern) | Flera jobb körs samtidigt | Resurskonflikter och jobbfel | Hög |
| [Schemalagd jobbdensitet](#scheduled-density) | Många datauppsättningar med grupper grupperade på samma timme | Flaskhalsar i rörledning och ofullständig segmentering | Hög |
| [Överdrivna batchar per datamängd](#excessive-batches-per-dataset) | En enda datauppsättning med dussintals dagliga batchar | Ineffektiv behandling och komplex drift | Medium |

## Schemaöverlappning {#schedule-overlap-pattern}

**Inslagsallvarlighetsgrad**: Hög | **Primär utgåva**: Resurskonflikt

**Vad du ska söka efter**: Flera jobb har schemalagts att köras samtidigt eller i nära följd, särskilt när resursintensiva jobb överlappar varandra.

I det här exemplet kan du se batchbearbetningsjobb som körs samtidigt som ett schemalagt segmenteringsjobb. Detta skapar resurskonflikter eftersom båda åtgärderna kräver betydande processorkraft och minne.

**Varför detta är problematiskt**:

* **Resurskonvention**: När flera resursintensiva jobb körs samtidigt, konkurrerar de om systemresurser (CPU, minne, I/O), vilket gör att alla jobb körs långsammare.
* **Oförutsägbara prestanda**: Jobbvaraktigheten blir inkonsekvent, vilket gör det svårt att planera tillförlitliga scheman.
* **Överlappande fördröjningar**: Om jobben tar längre tid än förväntat kan de fördröja underordnade jobb, vilket skapar en krusningseffekt genom hela pipeline.
* **Ökad felrisk**: Resursöverbelastningen kan orsaka timeout eller fel helt.

**Så här åtgärdar du det**:

* **Starkare jobbscheman**: Se till att resurskrävande åtgärder körs sekventiellt i stället för samtidigt.
* **Lägg till bufferttid**: Lämna tillräckligt med utrymme mellan jobb för att ta hänsyn till bearbetning av variationer.
* **Granska beroenden**: Identifiera vilka jobb som måste slutföras innan andra kan starta säkert.

## Schemalagd jobbdensitet {#scheduled-density}

**Inslagsallvarlighetsgrad**: Hög | **Primär fråga**: Flaskhalsar i pipeline

**Vad du ska leta efter**: För många datauppsättningar med flera grupper schemalagda inom samma timme, särskilt när dessa grupper ligger nära varandra och schemaläggs nära kritiska bearbetningsfönster som starttider för segmentering.

I det här mönstret ser du:

* Flera datamängder som kör flera batchar per dag
* ETL-jobb (intag av data i sjön och intag av profiler) klustrade inom samma timme
* Batchförbrukning schemalagd direkt före eller under schemalagda segmenteringsfönster

**Varför detta är problematiskt**:

* **Flaskhalsar i pipeline**: När flera batchar från olika datauppsättningar lagras i ett kort tidsfönster skapas en flaskhals som kan överbelasta matningsflödet.
* **Försenad profiltillgänglighet**: Profilinmatningsjobb som körs för nära starttiderna för segmentering kanske inte slutförs i tid, vilket resulterar i ofullständiga eller inaktuella målgruppsutvärderingar.
* **Oförutsebar segmentering**: Om det fortfarande körs uppströms ingessionsjobb när segmenteringen börjar, riskerar du att utvärdera målgrupper mot ofullständiga data, vilket leder till felaktigt målgruppsmedlemskap.
* **Överlappande fel**: En enstaka fördröjd batch i ett tätt skiktat schema kan orsaka en dominoeffekt, vilket försenar alla efterföljande batchar och efterföljande processer.
* **Resursbegränsning**: Det kan vara svårt att allokera tillräckligt med resurser vid bearbetning av för många samtidiga förtäringsjobb, vilket leder till långsammare bearbetningstider eller fel.

**Så här åtgärdar du det**:

* **Konsolidera batchar**: Minska batchfrekvensen genom att kombinera flera små batchar i färre, större batchar per datauppsättning.
* **Distribuera jämnt**: Sprid över intag-jobb under dagen i stället för att gruppera dem på specifika timmar.
* **Lägg till bufferttid**: Se till att det finns minst 1-2 timmars buffert mellan slutförande av profilinmatning och start av segmentering.
* **Granska krav**: Utvärdera om alla datauppsättningar verkligen behöver flera dagliga batchar - många fall fungerar med mindre frekventa uppdateringar.

## Överdrivna batchar per datamängd {#excessive-batches-per-dataset}

**Effektallvarlighetsgrad**: Medium | **Primärt problem**: Otillräcklig bearbetning

**Vad du ska leta efter**: En enskild datauppsättning med ett stort antal enskilda batchjobb som schemaläggs under dagen, vilket skapar en lång vertikal hög med jobb på tidslinjen.

I det här mönstret visas en datauppsättningsrad med många enskilda batchbearbetningsjobb som schemaläggs med täta intervall, ibland dussintals batchar per dag för en enskild datauppsättning.

**Varför detta är problematiskt**:

* **Ineffektiv bearbetning**: Varje batchjobb har overheadkostnader (initiering, validering, metadatauppdateringar). Bearbetning av många små satser är betydligt mindre effektivt än bearbetning av färre större batchar.
* **Ökad felyta**: Fler jobb innebär fler felmöjligheter. Varje sats som inte godkänns kräver undersökning och eventuell ombearbetning.
* **Onödig systeminläsning**: Ofta små batchar håller systemet konstant igång med rutinuppgifter i stället för med själva databearbetningen, vilket minskar det totala dataflödet.
* **Försenad datatillgänglighet**: Paradoxalt, om du kör många små batchar kan fördröjas när data blir tillgängliga för efterföljande processer jämfört med konsoliderade batchar.
* **Svår inspektion**: Spåra lyckade och prestanda för dussintals enskilda batchjobb per datauppsättning och blir operativt komplex och tidskrävande.
* **Fördröjning för profilbearbetning**: Varje grupp för profilinmatning utlöser profilbearbetning. Ofta kan små batchar göra att profilbearbetningen körs nästan kontinuerligt, vilket förhindrar effektiv batchoptimering.

**Så här åtgärdar du det**:

* **Minska batchfrekvensen**: Konsolidera till färre batchar per dag per datauppsättning för de flesta användningsfall.
* **Öka batchstorleken**: Ackumulera fler data innan du utlöser ett intag istället för att omedelbart ta in.
* **Justera efter affärsbehov**: Verifiera om timuppdateringar verkligen krävs eller om det finns tillräckligt med daglig/två daglig uppdatering.
* **Använd direktuppspelning för realtid**: Byt till direktuppspelningsupptagning för verkliga realtidskrav i stället för att simulera det med frekventa batchar.

## Nästa steg {#next-steps}

När du har identifierat mönster i dina jobbscheman:

* Visa [jobbinformation](job-schedules-details.md) om du vill undersöka specifika datauppsättningar och jobbkörningar som kan orsaka problem.
* Granska [Översikt över jobbscheman](job-schedules.md) för att förstå gränssnittet och inspektionsfunktionerna.
* Lär dig mer om [gruppinläsning](../ingestion/batch-ingestion/overview.md) för att optimera dina scheman för datainläsning.
* Förstå [segmenteringsscheman](../segmentation/home.md) för att säkerställa korrekt timing för målgruppsutvärderingar.
* Utforska [övervakning av måldataflöden](../dataflows/ui/monitor-destinations.md) för att se om pipeline är synlig från början till slut.
