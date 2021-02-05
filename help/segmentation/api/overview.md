---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;API;api;
title: API-guide för segmenteringstjänst
topic: guide
description: Med API:t för segmenteringstjänsten kan utvecklare programmässigt hantera segmenteringsåtgärder i Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# API-guide för segmenteringstjänst

[!DNL Adobe Experience Platform Segmentation Service] gör att ni kan skapa segment och generera målgrupper  [!DNL Adobe Experience Platform] utifrån era  [!DNL Real-time Customer Profile] data.

API:t [!DNL Segmentation Service] innehåller flera slutpunkter som gör att du kan hantera dina segmenteringsåtgärder i [!DNL Experience Platform] programmatiskt. I det här översiktsdokumentet finns introduktioner på hög nivå för var och en av dessa slutpunkter samt länkar till tillhörande slutpunktsguider för mer information. Innan du läser de enskilda slutpunktsguiderna bör du läsa [komma igång-guiden](./getting-started.md) för att få viktig information om nödvändiga huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder, se [API-referens för segmenteringstjänst](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportera jobb

Exportjobb är asynkrona processer som används för att behålla målgruppsmedlemmar i datauppsättningar. Du kan använda slutpunkten `/export/jobs` för att hämta alla exportjobb, skapa ett nytt exportjobb, hämta information om ett specifikt exportjobb eller avbryta ett specifikt exportjobb.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för exportjobb](./export-jobs.md).

## Förhandsvisningar och uppskattningar

Förhandsvisningar innehåller en numrerad lista med kvalificeringsprofiler för en segmentdefinition, som gör att du kan jämföra resultaten med vad du förväntar dig. Du kan använda slutpunkten `/preview` för att skapa ett nytt förhandsgranskningsjobb eller leta upp resultaten av ett visst förhandsgranskningsjobb.

Uppskattningar ger statistisk information för segmentdefinitioner, t.ex. förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse. Du kan använda slutpunkten `/estimate` för att visa en uppskattning av en segmentdefinition.

Mer information om hur du använder dessa slutpunkter finns i [handboken för förhandsvisningar och uppskattningar av slutpunkter](./previews-and-estimates.md).

## Scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda slutpunkten `/config/schedules` för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken för scheman](./schedules.md).

## Segmentdefinitioner

Segmentdefinitioner definierar vilka profiler som ska ingå i vilka målgruppssegment. Du kan använda slutpunkten `/segment/definitions` för att hantera segmentdefinitioner.

Mer information om hur du använder den här slutpunkten finns i [stödlinjen för segmentdefinitioner](./segment-definitions.md).

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera ett målgruppssegment. Du kan använda slutpunkten `/segment/jobs` för att hantera segmentjobb.

Mer information om hur du använder den här slutpunkten finns i [segmentjobbslutpunktsguiden](./segment-jobs.md).

## Segmentsökning

Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med segmentsökning finns i [guiden för sökslutpunkt](segment-search.md)

## Nästa steg

Om du vill komma igång med API:t [!DNL Segmentation Service] granskar du de olika slutpunktsguiderna för detaljerade anvisningar om hur du anropar tjänstens olika slutpunkter. Mer information om hur du arbetar med segment med hjälp av användargränssnittet i [!DNL Platform] finns i [användarhandboken för segmentering](../ui/overview.md).