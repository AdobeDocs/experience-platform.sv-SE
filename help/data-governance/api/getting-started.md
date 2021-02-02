---
keywords: Experience Platform;hem;populära ämnen;DULE;Schedule
solution: Experience Platform
title: Komma igång med API:t för principtjänsten
topic: developer guide
description: Med hjälp av API:t för principtjänst kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för principtjänsten.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Komma igång med API:t [!DNL Policy Service]

Med API:t [!DNL Policy Service] kan du skapa och hantera olika resurser som är relaterade till Adobe Experience Platform [!DNL Data Governance]. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t [!DNL Policy Service].

## Förutsättningar

Det krävs en fungerande förståelse för de olika [!DNL Experience Platform]-tjänsterna som används i arbetet med datastyrningsfunktionerna för att du ska kunna använda utvecklarhandboken. Innan du börjar arbeta med [!DNL Policy Service API] bör du läsa dokumentationen för följande tjänster:

* [[!DNL Data Governance]](../home.md): Det ramverk som  [!DNL Experience Platform] genomdriver efterlevnad av dataanvändning.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Policy Service] innehåller exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering för att kunna anropa [!DNL Platform] slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Data Governance], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Kärna eller anpassade resurser

I API:t [!DNL Policy Service] kallas alla principer och marknadsföringsåtgärder antingen för `core` eller `custom`-resurser.

`core` är de resurser som definieras och underhålls av Adobe, medan  `custom` resurser är de som skapas och underhålls av organisationen, och därför är unika och synliga enbart för IMS-organisationen. Därför är listnings- och uppslagsåtgärder (`GET`) de enda åtgärder som tillåts för `core`-resurser, medan listnings-, uppslags- och uppdateringsåtgärder (`POST`, `PUT`, `PATCH` och `DELETE`) är tillgängliga för `custom`-resurser.

## Nästa steg

Om du vill börja ringa anrop med hjälp av API:t för principtjänsten väljer du en av de tillgängliga slutpunktsguiderna.