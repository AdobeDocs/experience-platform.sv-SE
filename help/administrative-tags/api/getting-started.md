---
solution: Experience Platform
title: Komma igång med Unified Tags API
description: Följande dokumentation innehåller ytterligare information som du behöver känna till för att kunna arbeta med API:t för enhetliga taggar.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Komma igång med Unified Tags API {#getting-started}

Med API:t för enhetliga taggar kan du kategorisera och hantera dina affärsobjekt i Adobe Experience Platform.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med API:t för enhetliga taggar.

## Läser exempel-API-anrop

API-dokumentationen för enhetliga taggar innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa plattformsslutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i Experience Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådor](../../sandboxes/home.md).

## Nästa steg

Om du vill ringa anrop med API:t för enhetliga taggar väljer du en av de tillgängliga slutpunktsguiderna antingen med hjälp av den vänstra navigeringen eller i översikten för [utvecklarhandboken](./overview.md)
