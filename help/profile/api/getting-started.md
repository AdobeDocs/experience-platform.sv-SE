---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Komma igång med Real-Time Customer Profile API
type: Documentation
description: Komma igång-guiden för profil-API:t visar de nyckelbegrepp och grundläggande funktioner som du behöver känna till för att kunna använda API-slutpunkter för kundprofil i realtid för att utföra grundläggande CRUD-åtgärder mot profildata.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Komma igång med [!DNL Real-Time Customer Profile] API {#getting-started}

Med API-slutpunkter för kundprofil i realtid kan du utföra grundläggande CRUD-åtgärder mot profildata, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller batchar.

Att använda utvecklarhandboken kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som arbetar med [!DNL Profile] data. Innan du börjar arbeta med [!DNL Real-Time Customer Profile] API, läs dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile]](../home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Används för att skapa målgrupper utifrån kundprofildata i realtid.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ringa [!DNL Profile] API-slutpunkter.

## Läser exempel-API-anrop

The [!DNL Real-Time Customer Profile] API-dokumentationen innehåller exempel på API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de rubriker som krävs i [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla förfrågningar med en nyttolast i begärandetexten (t.ex. samtal av typen POST, PUT och PATCH) måste innehålla en `Content-Type` header. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## Nästa steg

Börja ringa samtal med [!DNL Real-Time Customer Profile] API: välj en av de tillgängliga slutpunktsguiderna.
