---
title: API-guide för segmenteringstjänst
description: Med API:t för segmenteringstjänsten kan utvecklare programmässigt hantera segmenteringsåtgärder i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: af79493c831c401c0bf14e391eb36a8175b4a2dd
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 2%

---

# API-guide för segmenteringstjänst

Med Adobe Experience Platform [!DNL Segmentation Service] kan du skapa målgrupper genom segmentdefinitioner eller andra källor i Adobe Experience Platform utifrån dina [!DNL Real-Time Customer Profile]-data.

API:t [!DNL Segmentation Service] innehåller flera slutpunkter som gör att du kan hantera dina segmenteringsåtgärder i [!DNL Experience Platform] programmatiskt. I det här översiktsdokumentet finns introduktioner på hög nivå för var och en av dessa slutpunkter samt länkar till tillhörande slutpunktsguider för mer information. Innan du läser de enskilda slutpunktsguiderna bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information om nödvändiga huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder läser du [API-referensen för segmenteringstjänsten](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Målgrupper

Målgrupper är en samling personer som delar liknande beteenden och/eller egenskaper. Dessa kan genereras antingen med Experience Platform eller från externa källor. Du kan använda slutpunkten `/audiences` för att hämta alla målgrupper, skapa en ny målgrupp, hämta information om en viss målgrupp, uppdatera en viss målgrupp eller ta bort en viss målgrupp.

Mer information om hur du använder den här slutpunkten finns i [målgruppsguiden](./audiences.md).

## Exportera jobb

Exportjobb är asynkrona processer som används för att behålla målgruppsmedlemmar i datauppsättningar. Du kan använda slutpunkten `/export/jobs` för att hämta alla exportjobb, skapa ett nytt exportjobb, hämta information om ett specifikt exportjobb eller avbryta ett specifikt exportjobb.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för exportjobb](./export-jobs.md).

## Externa målgrupper

Du kan importera externa målgrupper till Experience Platform, hämta en målgrupps skapandestatus, uppdatera en extern målgrupp, starta en målgruppsinspektion, hämta en extern målgruppsinmatningsstatus, lista målgruppsinmatningar och ta bort en extern målgrupp med slutpunkten `/core/ais/external-audiences`.

Mer information om hur du använder den här slutpunkten finns i [handboken för externa målgrupper](./external-audiences.md).

## Förhandsvisningar och uppskattningar

Förhandsvisningar innehåller en numrerad lista med kvalificeringsprofiler för en segmentdefinition, som gör att du kan jämföra resultaten med vad du förväntar dig. Du kan använda slutpunkten `/preview` för att skapa ett nytt förhandsgranskningsjobb eller leta upp resultaten av ett visst förhandsgranskningsjobb.

Uppskattningar ger statistisk information för segmentdefinitioner, t.ex. förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse. Du kan använda slutpunkten `/estimate` för att visa en uppskattning av en segmentdefinition.

Mer information om hur du använder dessa slutpunkter finns i guiden [Förhandsvisningar och uppskattningar av slutpunkter](./previews-and-estimates.md).

## Scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda slutpunkten `/config/schedules` för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

Mer information om hur du använder den här slutpunkten finns i guiden [Schemalägg slutpunkt](./schedules.md).

## Segmentdefinitioner

Segmentdefinitioner definierar vilka profiler som ska ingå i vilken målgrupp. Du kan använda slutpunkten `/segment/definitions` för att hantera segmentdefinitioner.

Mer information om hur du använder den här slutpunkten finns i [guiden för segmentdefinitioner](./segment-definitions.md).

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera en målgrupp. Du kan använda slutpunkten `/segment/jobs` för att hantera segmentjobb.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för segmentjobb](./segment-jobs.md).

## Segmentsökning

Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med segmentsökning finns i [guiden för sökslutpunkter](segment-search.md)

## Nästa steg

Om du vill komma igång med API:t [!DNL Segmentation Service] går du igenom de olika slutpunktsguiderna för att få detaljerade anvisningar om hur du anropar tjänstens olika slutpunkter. Mer information om hur du arbetar med segment med användargränssnittet för [!DNL Experience Platform] finns i [Användarhandboken för segmentering](../ui/overview.md).
