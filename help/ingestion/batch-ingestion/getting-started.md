---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Komma igång med API:t för datainmatning
type: Documentation
description: Komma igång-guiden för API:t för datainmatning visar de viktigaste koncept och grundläggande funktioner som du behöver känna till innan du kan börja importera data till Experience Platform med API:er.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Komma igång med API för datainmatning {#getting-started}

Med API-slutpunkter för datainmatning kan du utföra grundläggande CRUD-åtgärder för att importera data i Adobe Experience Platform.

API-guiderna kräver en fungerande förståelse för flera Adobe Experience Platform-tjänster som arbetar med data. Innan du använder API:t för datainmatning bör du läsa dokumentationen för följande tjänster:

* [Batchförtäring](./overview.md): Gör att du kan importera data till Adobe Experience Platform som gruppfiler.
* [[!DNL Real-Time Customer Profile]](../home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ringa [!DNL Profile] API-slutpunkter.

## Läser exempel-API-anrop

API-dokumentationen för datainmatning innehåller exempel på API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de rubriker som krävs i [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla förfrågningar med en nyttolast i begärandetexten (t.ex. samtal av typen POST, PUT och PATCH) måste innehålla en `Content-Type` header. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).
