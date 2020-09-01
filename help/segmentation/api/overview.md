---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;API;api;
solution: Adobe Experience Platform
title: Utvecklarhandbok för Adobe Experience Platform Segmentation Service
topic: guide
translation-type: tm+mt
source-git-commit: 0783979afa63890c77fd08f2d2ace4e141f59395
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Utvecklarhandbok för Adobe Experience Platform [!DNL Segmentation Service] API

[!DNL Adobe Experience Platform Segmentation Service] gör att ni kan skapa segment och generera målgrupper i [!DNL Adobe Experience Platform] utifrån era [!DNL Real-time Customer Profile] data.

API:t innehåller flera slutpunkter som du kan använda för att programmässigt hantera dina segmenteringsåtgärder i [!DNL Segmentation Service] [!DNL Experience Platform]. I det här översiktsdokumentet finns introduktioner på hög nivå för var och en av dessa slutpunkter samt länkar till tillhörande slutpunktsguider för mer information. Innan du läser de enskilda slutpunktsguiderna bör du läsa [Komma igång-guiden](./getting-started.md) för att få viktig information om vilka huvuden som behövs, läsa exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder, se API-referens för [segmenteringstjänsten](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportera jobb

Exportjobb är asynkrona processer som används för att behålla målgruppsmedlemmar i datauppsättningar. Du kan använda slutpunkten för att `/export/jobs` hämta alla exportjobb, skapa ett nytt exportjobb, hämta information om ett specifikt exportjobb eller avbryta ett specifikt exportjobb.

Mer information om hur du använder den här slutpunkten finns i slutpunktshandboken för [exportjobb](./export-jobs.md).

## Förhandsvisningar och uppskattningar

Förhandsvisningar innehåller en numrerad lista med kvalificeringsprofiler för en segmentdefinition, som gör att du kan jämföra resultaten med vad du förväntar dig. Du kan använda `/preview` slutpunkten för att skapa ett nytt förhandsgranskningsjobb eller leta upp resultatet av ett visst förhandsgranskningsjobb.

Uppskattningar ger statistisk information för segmentdefinitioner, t.ex. förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse. Du kan använda `/estimate` slutpunkten för att visa en uppskattning av en segmentdefinition.

Mer information om hur du använder dessa slutpunkter finns i guiden [för](./previews-and-estimates.md)förhandsvisningar och uppskattningar av slutpunkter.

## Scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda `/config/schedules` slutpunkten för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandboken](./schedules.md)för scheman.

## Segmentdefinitioner

Segmentdefinitioner definierar vilka profiler som ska ingå i vilka målgruppssegment. Du kan använda `/segment/definitions` slutpunkten för att hantera segmentdefinitioner.

Mer information om hur du använder den här slutpunkten finns i guiden [för](./segment-definitions.md)segmentdefinitioner.

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera ett målgruppssegment. Du kan använda `/segment/jobs` slutpunkten för att hantera segmentjobb.

Mer information om hur du använder den här slutpunkten finns i slutpunktshandboken för [segmentjobb](./segment-jobs.md).

## Segmentsökning

Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med segmentsökning finns i guiden [för sökslutpunkter](segment-search.md)

## Nästa steg

Om du vill komma igång med [!DNL Segmentation Service] API:t går du igenom de olika slutpunktsguiderna för att få detaljerade anvisningar om hur du anropar tjänstens olika slutpunkter. Mer information om hur du arbetar med segment med [!DNL Platform] användargränssnittet finns i användarhandboken för [segmentering](../ui/overview.md).