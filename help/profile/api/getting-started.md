---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Komma igång med kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: 6df3e6579139f01d9877c1f033ea7721ca78118c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# Komma igång med [!DNL Real-time Customer Profile] API {#getting-started}

Med API:t kan du utföra grundläggande CRUD-åtgärder mot profilresurser, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller grupper. [!DNL Real-time Customer Profile]

Att använda utvecklarhandboken kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som arbetar med [!DNL Profile] data. Innan du börjar arbeta med API:t bör du läsa dokumentationen för följande tjänster: [!DNL Real-time Customer Profile]

* [!DNL Real-time Customer Profile](../home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [!DNL Adobe Experience Platform Identity Service](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
* [!DNL Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API- [!DNL Profile] slutpunkter.

## Läser exempel-API-anrop

API-dokumentationen innehåller exempel på API-anrop som visar hur begäranden formateras korrekt. [!DNL Real-time Customer Profile] Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden med en nyttolast i begärandetexten (till exempel anrop till POST, PUT och PATCH) måste innehålla en `Content-Type` rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## Nästa steg

Om du vill börja ringa anrop med API:t väljer du en av de tillgängliga slutpunktsguiderna. [!DNL Real-time Customer Profile]