---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Komma igång med Real-Time Customer Profile API
type: Documentation
description: Komma igång-guiden för profil-API:t visar de nyckelbegrepp och grundläggande funktioner som du behöver känna till för att kunna använda API-slutpunkter för kundprofil i realtid för att utföra grundläggande CRUD-åtgärder mot profildata.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Komma igång med [!DNL Real-Time Customer Profile]-API:t {#getting-started}

Med API-slutpunkter för kundprofil i realtid kan du utföra grundläggande CRUD-åtgärder mot profildata, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller batchar.

Om du vill använda utvecklarhandboken måste du ha en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för att arbeta med [!DNL Profile]-data. Innan du börjar arbeta med API:t [!DNL Real-Time Customer Profile] bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile]](../home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Gör att du kan skapa målgrupper från kundprofildata i realtid.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API-slutpunkter för [!DNL Profile].

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Real-Time Customer Profile] innehåller exempel på API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Experience Platform]-slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Begäranden till [!DNL Experience Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden med en nyttolast i begärandetexten (som POST-, PUT- och PATCH-anrop) måste innehålla en `Content-Type`-rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Real-Time Customer Profile] väljer du en av de tillgängliga slutpunktsguiderna.
