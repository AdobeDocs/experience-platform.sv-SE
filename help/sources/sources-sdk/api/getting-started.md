---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
solution: Experience Platform
title: Komma igång med SDK-källor (beta)
topic-legacy: developer guide
description: Det här dokumentet innehåller en introduktion till den information som krävs innan du försöker skapa en ny källa med hjälp av Sources SDK.
hide: true
hidefromtoc: true
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Komma igång med SDK-källor (beta)

>[!IMPORTANT]
>
>SDK:n för källor är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Med Sources SDK kan du integrera din egen REST-baserade källa för att överföra data till Adobe Experience Platform. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Förutsättningar

Om du vill använda Sources SDK måste du se till att du har tillgång till en IMS-organisationssandlåda som har etablerats med Adobe Experience Platform Sources.

Handboken kräver även en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

SDK för källorna och [!DNL Flow Service] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i Platform, inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i plattformen finns i [sandlådedokumentation](../../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Nästa steg

För att börja skapa en ny källa med Sources SDK, se självstudiekursen om [skapa en ny källa](./create.md).
