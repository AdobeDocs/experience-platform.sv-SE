---
keywords: Experience Platform;home;popular topics;DULE;dule
solution: Experience Platform
title: Komma igång med API:t för principtjänsten
topic: developer guide
description: Med hjälp av API:t för principtjänst kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t för principtjänsten.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Komma igång med [!DNL Policy Service] API

Med API:t kan du [!DNL Policy Service] skapa och hantera olika resurser för Adobe Experience Platform [!DNL Data Governance]. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna till innan du försöker anropa [!DNL Policy Service] API:t.

## Förutsättningar

Att använda utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som används i arbetet med datastyrningsfunktionerna. Innan du börjar arbeta med [!DNL Policy Service API]programmet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Data Governance]](../home.md): Ramverket som [!DNL Experience Platform] genomdriver efterlevnad av dataanvändning.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. [!DNL Policy Service] Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Data Governance], isoleras till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Kärna eller anpassade resurser

I API:t [!DNL Policy Service] kallas alla policyer och marknadsföringsåtgärder antingen `core` eller `custom` resurser.

`core` Resurserna är de som definieras och underhålls av Adobe, medan `custom` resurser är de som skapas och underhålls av organisationen och därför är unika och synliga enbart för IMS-organisationen. Därför är listnings- och uppslagsåtgärder (`GET`) de enda åtgärder som tillåts för `core` resurser, medan listnings-, uppslags- och uppdateringsåtgärder (`POST`, `PUT`, `PATCH`och `DELETE`) är tillgängliga för `custom` resurser.

## Nästa steg

Om du vill börja ringa anrop med hjälp av API:t för principtjänsten väljer du en av de tillgängliga slutpunktsguiderna.