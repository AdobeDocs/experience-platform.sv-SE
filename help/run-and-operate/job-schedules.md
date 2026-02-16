---
description: Lär dig hur du inspekterar och felsöker schemalagda batchbearbetningsjobb med verktyget Jobbscheman i Adobe Experience Platform.
solution: Experience Platform
title: Inspektera jobbscheman
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# Granska jobbscheman

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] är för närvarande tillgängligt som en begränsad version och endast för följande Real-Time CDP-jobb:
>
> * Intag av batchdata i sjö
> * Inmatning av gruppprofil
> * Grupputleverans
> * Aktivering av batchmål.

[!UICONTROL Job Schedules] ger en enhetlig vy över alla schemalagda batchbearbetningsjobb i hela dataredjan, från inmatning till målaktivering. Kontrollera körningsstatus, identifiera schemaläggningskonflikter och diagnostisera konfigurationsproblem innan de påverkar din affärsverksamhet.

Använd Jobbscheman för att undersöka fel, optimera jobbtiming och förstå beroenden mellan inmatning av data i sjön, profilbearbetning, segmentering och målaktivering. Mer information om hur du löser vanliga konfigurationsproblem finns i dokumentationen om [identifiering av antimönster för jobbscheman](job-schedules-anti-patterns.md).

## Förhandskrav {#prerequisites}

Om du vill komma åt [!UICONTROL Job Schedules] behöver du behörigheterna **[!UICONTROL View Job Schedules]** och **[!UICONTROL View Profile Management]** [åtkomstkontroll](/help/access-control/home.md#permissions).

Kontakta systemadministratören för att kontrollera att du har rätt behörigheter.

## Komma igång {#getting-started}

Innan du använder [!UICONTROL Job Schedules] bör du känna till följande Experience Platform-koncept:

* **[Batchförtäring](../ingestion/batch-ingestion/overview.md)**: Hur data läses in i datasjön och profilarkivet i schemalagda intervall.
* **[Segmentering](../segmentation/home.md)**: Hur målgrupper utvärderas och uppdateras baserat på profildata och segmentdefinitioner.
* **[Kundprofil i realtid](../profile/home.md)**: Hur profildata är enhetliga och tillgängliga för segmentering och aktivering.
* **[Destinationer](../destinations/home.md)**: Var och hur data aktiveras för system och marknadsföringsplattformar i senare led.

Genom att förstå de här komponenterna kan du tolka jobbkörningsmönster och diagnostisera problem när de inträffar.

## Om gränssnittet Jobbscheman {#understanding-interface}

Så här kommer du åt [!UICONTROL Job Schedules]:

1. I Experience Platform-gränssnittet väljer du **[!UICONTROL Run and Operate]** i den vänstra navigeringen.
2. Välj **[!UICONTROL Job Schedules]**.

Sidan [!UICONTROL Job Schedules] innehåller en översikt över alla schemalagda batchbearbetningsjobb.

![Kör och använd vänster navigering](assets/job-schedules/run-and-operate-left-nav.png)

### Sammanfattningskort {#summary-cards}

Överst på sidan finns sammanfattningskort med snabba insikter om batchbearbetningen.

![Sammanfattningskort för jobbscheman som visar insikter i batchbearbetningsjobb](assets/job-schedules/job-schedules-cards.png)

* **Intrågningen i sjön körs**: Antalet infogningsjobb i sjön som har körts.
* **Inläsning av profil körs**: Antalet profilinmatningsjobb som har körts.
* **Nästa segmentering**: När nästa schemalagda segmenteringsjobb körs.
* **Nästa målaktivering**: När nästa schemalagda målaktiveringsjobb körs.

Dessa kort hjälper er att förstå aktiviteten och kommande scheman i hela dataredjan. Värdena för **sjöintagning kör** och **profilåtkomsten kör** ändring baserat på det valda tidsintervallet (i dag, i går eller senaste 7 dagarna). Nästa körningskort (**Nästa segmentering** och **Nästa målaktivering**) påverkas inte av tidsväljaren.

### Tidsväljare {#time-period}

Använd tidsperiodväljarna för att välja hur långt tillbaka de schemalagda jobben ska visas.

![Animerat exempel på användargränssnittet för tidsperiodväljaren i jobbscheman](assets/job-schedules/time-selector.gif)

* **I dag**: Visa jobb som är schemalagda i dag (standardvy).
* **I går**: Visa jobb som kördes i går.
* **De senaste 7 dagarna**: Visa jobb från den senaste veckan.

### Information om batchjobbscheman {#job-schedules-details}

Huvudvyn visar när batchjobben är schemalagda att köras under dagen. Du kan:

* **Visa jobb efter datauppsättning eller entitet**: Den vänstra kolumnen visar namnen på datauppsättningar eller bearbetningsjobb (till exempel datauppsättningar för inmatning eller segmenteringsjobb).
* **Se jobbtiming**: Tidslinjen visar när varje jobb är schemalagt att köras, med visuella indikeringar som markerar den schemalagda tiden.
* **Filtrera jobb**: Använd filterikonen för att begränsa vilka datauppsättningar som ska inkluderas i rapporten.
* **Förstå jobbtyper**: Den färgkodade teckenförklaringen längst ned hjälper dig att identifiera olika jobbtyper:
   * **Intag av sjön** (grönt): Intag av data i sjön
   * **Intag av profiler** (rosa): Intag av data i profilarkivet
   * **Segmentering** (ljusblå): Målgruppsutvärderingsjobb
   * **Profilexport** (blå): Exportera profildata
   * **Aktivering** (mörkgrå): Målaktiveringsjobb
   * **Pågår** (randig): Jobb som körs eller står i kö

I den här tidslinjevyn kan du identifiera schemaläggningskonflikter, förstå beroenden mellan jobb och optimera batchbearbetningsscheman.

## Identifiera konfigurationsproblem {#identifying-issues}

När du granskar dina jobbscheman kan du se mönster som indikerar konfigurationsproblem. Vanliga problem är:

* Jobb som schemalagts för att hålla ihop, orsakar resurskonflikter
* För många batchar som körs i samma tidsfönster
* Enskilda datauppsättningar med stora dagliga batchjobb
* Inmatningsjobb som schemaläggs omedelbart innan segmentering körs

Dessa mönster kan leda till jobbfel, ofullständig databehandling och dålig systemprestanda. Mer information om hur du identifierar och löser dessa problem finns i dokumentationen om [identifiering av mönster för jobbalbum](job-schedules-anti-patterns.md).

När du behöver undersöka specifika datauppsättningar eller jobbkörningar kan du fördjupa dig i detaljerade vyer för att se körningshistorik, felmeddelanden, prestandamätningar och beroenden. Mer information om hur du visar detaljerade data finns i dokumentationen om [att visa jobbinformation](job-schedules-details.md).


## Nästa steg {#next-steps}

När du har lärt dig mer om jobbscheman kan du utforska följande relaterade ämnen:

* [Visa jobbinformation](job-schedules-details.md): Lär dig mer om hur du detaljerar enskilda datauppsättningar och jobbkörningar för detaljerad utredning.
* [Identifiera kantmönster för jobbschema](job-schedules-anti-patterns.md): Lär dig hur du identifierar och löser vanliga konfigurationsproblem som påverkar pipeline-prestanda.
* [Gruppinmatning](../ingestion/batch-ingestion/overview.md): Lär dig hur du importerar data till Experience Platform med gruppbearbetning.
* [Segmentering](../segmentation/home.md): Förstå hur målgrupper utvärderas och uppdateras med schemalagda intervall.
* [Övervaka dataflöden för mål](../dataflows/ui/monitor-destinations.md): Lär dig övervaka dataflöden för målaktivering.
* [Schemalägg målgruppsexport](../destinations/ui/activate-batch-profile-destinations.md): Lär dig hur du konfigurerar schemalagda målaktiveringar för batch.
