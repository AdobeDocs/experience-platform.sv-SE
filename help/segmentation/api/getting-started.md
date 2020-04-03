---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för segmenteringstjänst
topic: developer guide
translation-type: tm+mt
source-git-commit: 38762fa57188ed018c4347c07765f3d09daef2e6

---


# Utvecklarhandbok för segmenteringstjänst

Med segmentering kan ni skapa segment och generera målgrupper i Adobe Experience Platform utifrån era kundprofildata i realtid.

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänsterna som är kopplade till användningen av segmentering.

- [Segmentering](../home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
- [Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
- [Kundprofil](../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Sandlådor](../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna använda segmentering med API.

### Läser exempel-API-anrop

API-dokumentationen för segmenteringstjänsten innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa plattformsslutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de huvuden som krävs i API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>**Obs!** Mer information om hur du arbetar med sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

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

For more information on using this endpoint, please read the [schedules developer guide](./schedules.md).

## Segment definitions

Segment definitions define which profiles will be part of which audience segments. You can use the `/segment/definitions` endpoint to retrieve a list of segment definitions, create a new segment definition, retrieve details of a specific segment definition, delete a specific segment definition, or overwrite details of a specific segment definition.

For more information on using this endpoint, please read the [segment definitions developer guide](./segment-definitions.md). -->

## Segmentjobb

Segmentjobb bearbetar tidigare etablerade segmentdefinitioner för att generera ett målgruppssegment. Du kan använda `/segment/jobs` slutpunkten för att hämta en lista med segmentjobb, skapa ett nytt segmentjobb, hämta information om ett specifikt segmentjobb eller ta bort ett specifikt segmentjobb.

Mer information om hur du använder den här slutpunkten finns i utvecklarhandboken för [segmentjobb](./segment-jobs.md).

## Nästa steg

Om du vill börja ringa anrop med segmenterings-API:t väljer du en av delguiderna för att lära dig hur du använder specifika segmenteringsrelaterade slutpunkter. Mer information om hur du arbetar med segment med hjälp av användargränssnittet för plattformen finns i användarhandboken för [segmentering](../ui/overview.md).