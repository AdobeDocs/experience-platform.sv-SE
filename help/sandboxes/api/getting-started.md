---
keywords: Experience Platform;home;populära topics;sandbox developguide
solution: Experience Platform
title: Komma igång med sandbox-API
description: Med sandbox-API kan utvecklare programmässigt hantera sandlådor i Adobe Experience Platform. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# Komma igång med sandbox-API

Sandlådor i Adobe Experience Platform har isolerade utvecklingsmiljöer där du kan testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka produktionsmiljön.

Den här utvecklarhandboken innehåller steg som hjälper dig att använda sandbox-API:t för att hantera sandlådor i Experience Platform, och innehåller exempel på API-anrop för att utföra olika åtgärder.

## Förhandskrav

För att kunna hantera sandlådor för din organisation måste du ha administratörsbehörighet för sandlådan. Användare utan åtkomstbehörighet kan bara använda [tillgängliga sandlådeslutpunkter](./available.md) för att lista aktiva sandlådor för den aktuella användaren. Mer information om hur du tilldelar sandlådebehörigheter för Experience Platform finns i [åtkomstkontrollsöversikten](../../access-control/home.md).

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

Den här guiden kräver att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa Experience Platform API:er. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Experience Platform API-anrop, vilket visas nedan:

* Behörighet: Bärare `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Förutom autentiseringshuvuden kräver alla begäranden en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT och PATCH) kräver ytterligare ett huvud:

* Content-Type: application/json

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran som visar nödvändiga huvuden och korrekt formaterade nyttolaster samt ett exempelsvar för ett lyckat anrop.
