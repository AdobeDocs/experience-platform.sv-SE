---
keywords: Experience Platform;hem;populära ämnen;Attributbaserad åtkomstkontroll;attributbaserad åtkomstkontroll
title: Komma igång med den attributbaserade åtkomstkontrollen
description: Med den attributbaserade åtkomstkontrollen kan du programmässigt hantera roller och profiler i Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Komma igång med den attributbaserade åtkomstkontrollen

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll är för närvarande tillgänglig i en begränsad version för USA-baserade vårdkunder. Den här funktionen kommer att vara tillgänglig för alla Real-time Customer Data Platform-kunder när den släpps helt.

Den här utvecklarhandboken innehåller steg som hjälper dig att använda den attributbaserade åtkomstkontrollen för att hantera roller, produkter, behörighetskategorier och behörighetsgrupper i Adobe Experience Platform, och innehåller exempel på API-anrop för olika åtgärder.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

Den här guiden kräver att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa API:er för plattformen. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Förutom autentiseringshuvuden kräver alla begäranden en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT och PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Nästa steg

Nu när du har samlat in de nödvändiga inloggningsuppgifterna kan du nu fortsätta att läsa resten av utvecklarhandboken. Varje avsnitt innehåller viktig information om deras slutpunkter och visar exempel på API-anrop för att utföra CRUD-åtgärder. Varje anrop innehåller det allmänna API-formatet, en exempelbegäran som visar nödvändiga huvuden och korrekt formaterade nyttolaster samt ett exempelsvar för ett lyckat anrop.

Se följande API-självstudiekurser för att börja ringa anrop till det attributbaserade API:t för åtkomstkontroll:

* [Rollslutpunkt](./roles.md)
* [Slutpunkt för produkter](./products.md)
