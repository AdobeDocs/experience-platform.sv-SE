---
title: Komma igång med API för granskningsfråga
description: Med API:t för granskningsfråga kan du hämta mätdata för olika Adobe Experience Platform-funktioner. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för granskningsfråga.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Komma igång med API för granskningsfråga

Med Adobe Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner i form av loggar för granskningshändelser. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen.

Med API:t för granskningsfråga kan du granska användaraktivitet för olika tjänster och funktioner i form av granskningshändelseloggar. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för granskningsfråga.

## Förhandskrav

För att kunna hantera granskningshändelser måste du ha åtkomstkontrollsbehörigheten **[!UICONTROL View User Activity Log]** (finns under kategorin [!UICONTROL Data Governance]). Mer information om hur du hanterar individuella behörigheter för plattformsfunktioner finns i [åtkomstkontrollsdokumentationen](../../../../access-control/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

Den här guiden kräver att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa anrop till plattforms-API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bärare `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i. Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT och PATCH) kräver ytterligare en rubrik:

* Content-Type: application/json

## Nästa steg

Om du vill börja ringa anrop med API:t [!DNL Audit Query] kan du läsa [händelsens slutpunktshandbok](./events.md) och [exportens slutpunktshandbok](./export.md).
