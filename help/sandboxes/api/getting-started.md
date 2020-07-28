---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för sandbox-API
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Utvecklarhandbok för sandbox-API

Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön.

Den här utvecklarhandboken innehåller steg som hjälper dig att använda sandbox-API:t för att hantera sandlådor i Experience Platform, och innehåller exempel på API-anrop för att utföra olika åtgärder.

## Komma igång med sandbox-API

För att kunna hantera sandlådor för din IMS-organisation måste du ha administratörsbehörighet för sandlådan. Användare utan åtkomstbehörighet kan bara använda slutpunkten för att [visa aktiva sandlådor för den aktuella användaren](./list-active-sandboxes.md). Mer information om hur du tilldelar sandlådebehörigheter till Experience Platform finns i översikten över [](../../access-control/home.md) åtkomstkontrollen.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

Den här guiden kräver att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa Platform API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Förutom autentiseringshuvuden kräver alla begäranden en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT och PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna **API-formatet**, en **exempelbegäran** med obligatoriska huvuden och korrekt formaterade nyttolaster samt ett **exempelsvar** för ett lyckat anrop.