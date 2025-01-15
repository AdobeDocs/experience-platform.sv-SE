---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Komma igång med självbetjäningskällor (Batch SDK)
description: Det här dokumentet innehåller en introduktion till den information som krävs för att du ska kunna skapa en ny källa med självbetjäningskällor (Batch SDK).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Komma igång med självbetjäningskällor (Batch SDK)

Med självbetjäningskällor (Batch SDK) kan du integrera din egen REST-baserade källa för att skicka batchdata till Adobe Experience Platform. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Förhandskrav

Om du vill använda självbetjäningskällor (Batch SDK) måste du se till att du har tillgång till en sandlåda för en organisation som är etablerad med Adobe Experience Platform-källor.

Handboken kräver även en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

I API-dokumentationen för självbetjäningskällor (Batch SDK) och [!DNL Flow Service] finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i plattformen, inklusive de som tillhör [!DNL Flow Service], är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i [sandlådedokumentationen](../../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Nästa steg

Om du vill börja skapa en ny källa med självbetjäningskällor (Batch SDK) ska du titta i självstudiekursen [Skapa en ny källa](./create.md).
