---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Komma igång med kundprofils-API:t i realtid
topic: guide
type: Documentation
description: Komma igång-guiden för profil-API:t visar de nyckelbegrepp och grundläggande funktioner som du behöver känna till för att kunna använda API-slutpunkter för kundprofil i realtid för att utföra grundläggande CRUD-åtgärder mot profildata.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Komma igång med [!DNL Real-time Customer Profile] API {#getting-started}

Med hjälp av API-slutpunkter för kundprofil i realtid kan du utföra grundläggande CRUD-åtgärder mot profildata, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller batchar.

För att kunna använda utvecklarhandboken måste du ha en fungerande förståelse för de olika Adobe Experience Platform-tjänster som arbetar med [!DNL Profile]-data. Innan du börjar arbeta med API:t [!DNL Real-time Customer Profile] bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-time Customer Profile]](../home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API-slutpunkterna [!DNL Profile].

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Real-time Customer Profile] innehåller exempel-API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering för att kunna anropa [!DNL Platform] slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden med en nyttolast i begärandetexten (som anrop till POST, PUT och PATCH) måste innehålla en `Content-Type`-rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Real-time Customer Profile] väljer du en av de tillgängliga slutpunktsguiderna.