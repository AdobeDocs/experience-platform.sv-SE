---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för segmenteringstjänst
topic: developer guide
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Med Adobe Experience Platform segmenteringstjänst kan ni skapa segment och generera målgrupper i Adobe Experience Platform utifrån era [!DNL Real-time Customer Profile] data.

Utvecklarhandboken kräver en fungerande förståelse av de olika Experience Platform-tjänster som används [!DNL Segmentation Service].

- [!DNL Segmentation](../home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
- [!DNL Real-time Customer Profile](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med [!DNL Segmentation] API:t.

## Läser exempel-API-anrop

API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. [!DNL Segmentation Service] Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa Platform-slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform]finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

<!-- ## Estimates

Estimates provides statistical information for a segment definition, such as projected audience size and confidence interval. You can use the `/estimate` endpoint to view an estimate of a segment definition. 

For more information on using this endpoint, please read the [estimates developer guide](./estimates.md). 

## Export jobs

Export jobs are asynchronous processes that are used to persist audience segment members to datasets. You can use the `/export/jobs` endpoint to retrieve all export jobs, create a new export job, retrieve details of a specific export job, or cancel a specific export job.

For more information on using this endpoint, please read the [export jobs developer guide](./export-jobs.md).

## Previews

Previews provide a paginated list of qualifying profiles for a segment definition, allowing you to compare the results against what you expect. You can use the `/preview` endpoint to create a new preview job, look up results of a specific preview job, or delete a specific preview job.

For more information on using this endpoint, please read the [previews developer guide](./previews.md).

## PQL conversions

Profile Query Language (PQL) conversions allows you to convert your formatting between `pql/text` and `pql/json`. You can do this by using the `/segment/conversion` endpoint.

For more information on using this endpoint, please read the [PQL conversions developer guide](./pql-conversions.md).

## Schedules

Schedules are a tool that can be used to automatically run export jobs once a day. You can use the `/config/schedules` endpoint to retrieve a list of schedules, create a new schedule, retrieve details of a specific schedule, update a specific schedule, or delete a specific schedule. 

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md). -->

## Segmentdefinitioner

Segmentdefinitioner definierar vilka profiler som ska ingå i vilka målgruppssegment. Du kan använda `/segment/definitions` slutpunkten för att hämta en lista med segmentdefinitioner, skapa en ny segmentdefinition, hämta information om en viss segmentdefinition, ta bort en viss segmentdefinition eller skriva över information om en viss segmentdefinition.

Mer information om hur du använder den här slutpunkten finns i utvecklarhandboken för [segmentdefinitioner](./segment-definitions.md).

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera ett målgruppssegment. Du kan använda `/segment/jobs` slutpunkten för att hämta en lista med segmentjobb, skapa ett nytt segmentjobb, hämta information om ett specifikt segmentjobb eller ta bort ett specifikt segmentjobb.

Mer information om hur du använder den här slutpunkten finns i utvecklarhandboken för [segmentjobb](./segment-jobs.md).

## Segmentsökning

Segmentsökning används för att söka efter och indexera konfigurerbara fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med segmentsökning finns i [guiden för sökutvecklare](segment-search.md)

## Nästa steg

Om du vill ringa anrop med [!DNL Segmentation Service] API:t väljer du en av de tillgängliga slutpunktsguiderna med hjälp av den vänstra navigeringen eller i översikten för [utvecklarhandboken](./overview.md)