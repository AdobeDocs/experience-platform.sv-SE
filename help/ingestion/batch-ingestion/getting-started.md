---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Komma igång med API för datainmatning
type: Documentation
description: Komma igång-guiden för API:t för datainmatning visar de viktigaste koncept och grundläggande funktioner som du behöver känna till innan du kan börja importera data till Experience Platform med API:er.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Komma igång med API för datainmatning {#getting-started}

Med API-slutpunkter för datainmatning kan du utföra grundläggande CRUD-åtgärder för att importera data i Adobe Experience Platform.

API-guiderna kräver en fungerande förståelse för flera Adobe Experience Platform-tjänster som arbetar med data. Innan du använder API:t för datainmatning bör du läsa dokumentationen för följande tjänster:

* [Gruppinmatning](./overview.md): Gör att du kan importera data till Adobe Experience Platform som gruppfiler.
* [[!DNL Real-Time Customer Profile]](../home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API-slutpunkter för [!DNL Profile].

## Läser exempel-API-anrop

API-dokumentationen för datainmatning innehåller exempel på API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Experience Platform]-slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden med en nyttolast i begärandetexten (som POST-, PUT- och PATCH-anrop) måste innehålla en `Content-Type`-rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).
