---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Komma igång med kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Komma igång med kundprofils-API:t i realtid {#getting-started}

Med hjälp av API:t för kundprofil i realtid kan du utföra grundläggande CRUD-åtgärder mot profilresurser, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller batchar.

För att kunna använda utvecklarhandboken måste du ha en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används i arbetet med profildata. Innan du börjar arbeta med kundprofils-API:t i realtid bör du läsa dokumentationen för följande tjänster:

* [Kundprofil](../home.md)i realtid: Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
* [Segmenteringstjänsten](../../segmentation/home.md)Adobe Experience Platform: Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API-slutpunkter för profiler.

## Läser exempel-API-anrop

I dokumentationen för kundprofil i realtid finns exempel-API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa Platform-slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden med en nyttolast i begärandetexten (som POST-, PUT- och PATCH-anrop) måste innehålla en `Content-Type` rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## Nästa steg

Välj en av de tillgängliga slutpunktsguiderna för att börja ringa samtal med hjälp av kundprofils-API:t i realtid.