---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;API;api;
title: API-guide för segmenteringstjänst
topic-legacy: guide
description: Med API:t för segmenteringstjänsten kan utvecklare programmässigt hantera segmenteringsåtgärder i Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: b48ead4255d50585cd315436ccb9727d86142d4c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# API-guide för segmenteringstjänst

[!DNL Adobe Experience Platform Segmentation Service] kan ni skapa segment och generera målgrupper i [!DNL Adobe Experience Platform] från [!DNL Real-time Customer Profile] data.

The [!DNL Segmentation Service] API har flera slutpunkter som gör att du kan hantera din segmentering programmatiskt i [!DNL Experience Platform]. I det här översiktsdokumentet finns introduktioner på hög nivå för var och en av dessa slutpunkter samt länkar till tillhörande slutpunktsguider för mer information. Innan du läser de enskilda slutpunktsstödlinjerna, se [komma igång-guide](./getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder, se [API-referens för segmenteringstjänst](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Målgrupper

Målgrupper är en samling personer som delar liknande beteenden och/eller egenskaper. Dessa kan genereras antingen med Platform eller från externa källor. Du kan använda `/audiences` slutpunkt för att hämta alla målgrupper, skapa en ny målgrupp, hämta information om en viss målgrupp, uppdatera en viss målgrupp eller ta bort en viss målgrupp.

Mer information om hur du använder den här slutpunkten finns i [slutpunktsguide för målgrupper](./audiences.md).

## Exportera jobb

Exportjobb är asynkrona processer som används för att behålla målgruppsmedlemmar i datauppsättningar. Du kan använda `/export/jobs` slutpunkt för att hämta alla exportjobb, skapa ett nytt exportjobb, hämta information om ett specifikt exportjobb eller avbryta ett specifikt exportjobb.

Mer information om hur du använder den här slutpunkten finns i [slutpunktsguide för exportjobb](./export-jobs.md).

## Förhandsvisningar och uppskattningar

Förhandsvisningar innehåller en numrerad lista med kvalificeringsprofiler för en segmentdefinition, som gör att du kan jämföra resultaten med vad du förväntar dig. Du kan använda `/preview` slutpunkt för att skapa ett nytt förhandsgranskningsjobb eller för att slå upp resultatet av ett visst förhandsgranskningsjobb.

Uppskattningar ger statistisk information för segmentdefinitioner, t.ex. förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse. Du kan använda `/estimate` slutpunkt för att visa en uppskattning av en segmentdefinition.

Mer information om hur du använder dessa slutpunkter finns i [guide för förhandsgranskningar och uppskattningar av slutpunkter](./previews-and-estimates.md).

## Scheman

Scheman är ett verktyg som kan användas för att automatiskt köra batchsegmenteringsjobb en gång om dagen. Du kan använda `/config/schedules` slutpunkt för att hämta en lista med scheman, skapa ett nytt schema, hämta information om ett specifikt schema, uppdatera ett specifikt schema eller ta bort ett specifikt schema.

Mer information om hur du använder den här slutpunkten finns i [slutpunktshandbok för scheman](./schedules.md).

## Segmentdefinitioner

Segmentdefinitioner definierar vilka profiler som ska ingå i vilka målgruppssegment. Du kan använda `/segment/definitions` slutpunkt för att hantera segmentdefinitioner.

Mer information om hur du använder den här slutpunkten finns i [slutpunktsguide för segmentdefinitioner](./segment-definitions.md).

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera ett målgruppssegment. Du kan använda `/segment/jobs` slutpunkt för att hantera segmentjobb.

Mer information om hur du använder den här slutpunkten finns i [slutpunktsguide för segmentjobb](./segment-jobs.md).

## Segmentsökning

Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med segmentsökning finns i [sökslutpunktsguide](segment-search.md)

## Nästa steg

Så här kommer du igång med [!DNL Segmentation Service] API, gå igenom de olika slutpunktsguiderna för att få detaljerade anvisningar om hur du anropar tjänstens olika slutpunkter. Mer information om hur du arbetar med segment med [!DNL Platform] Gränssnitt, se [Användarhandbok för segmentering](../ui/overview.md).
