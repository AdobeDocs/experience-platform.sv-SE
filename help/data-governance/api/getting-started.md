---
keywords: Experience Platform;hem;populära ämnen;DULE;Schedule
solution: Experience Platform
title: Komma igång med API:t för principtjänsten
description: Med hjälp av API:t för principtjänst kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker ringa anrop till API:t för principtjänsten.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Komma igång med [!DNL Policy Service]-API:t

Med API:t [!DNL Policy Service] kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker anropa API:t [!DNL Policy Service].

## Förhandskrav

Om du vill använda utvecklarhandboken måste du ha en fungerande förståelse för de olika [!DNL Experience Platform]-tjänsterna som används i arbetet med datastyrningsfunktioner. Innan du börjar arbeta med [!DNL Policy Service API] bör du läsa dokumentationen för följande tjänster:

* [Datastyrning](../home.md): Ramverket som [!DNL Experience Platform] använder för att framtvinga efterlevnad av dataanvändning.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Policy Service] innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för att kunna anropa [!DNL Platform]-slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör Datastyrning, är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Kärna eller anpassade resurser

I API:t [!DNL Policy Service] kallas alla principer och marknadsföringsåtgärder antingen `core` eller `custom` resurser.

`core`-resurser är de som definieras och underhålls av Adobe, medan `custom`-resurser är de som skapas och underhålls av din organisation och därför är unika och synliga enbart för din organisation. Därför är listnings- och uppslagsåtgärder (`GET`) de enda åtgärder som tillåts för `core`-resurser, medan listnings-, uppslags- och uppdateringsåtgärder (`POST`, `PUT`, `PATCH` och `DELETE`) är tillgängliga för `custom`-resurser.

## Nästa steg

Välj en av de tillgängliga slutpunktsguiderna för att börja ringa anrop med hjälp av API:t för principtjänsten.
