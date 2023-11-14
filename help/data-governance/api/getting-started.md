---
keywords: Experience Platform;hem;populära ämnen;DULE;Schedule
solution: Experience Platform
title: Komma igång med API:t för principtjänsten
description: Med hjälp av API:t för principtjänst kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept som du behöver känna till innan du försöker ringa anrop till API:t för principtjänsten.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Komma igång med [!DNL Policy Service] API

The [!DNL Policy Service] Med API kan du skapa och hantera olika resurser för Adobe Experience Platform datastyrning. Det här dokumentet innehåller en introduktion till de centrala koncept du behöver känna innan du försöker ringa till [!DNL Policy Service] API.

## Förutsättningar

Att använda utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som används i arbetet med datastyrningsfunktioner. Innan du börjar arbeta med [!DNL Policy Service API], läs dokumentationen för följande tjänster:

* [Datastyrning](../home.md): Det ramverk som [!DNL Experience Platform] regelefterlevnad för dataanvändning.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

## Läser exempel-API-anrop

The [!DNL Policy Service] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de rubriker som krävs i [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör datastyrning, isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

## Kärna eller anpassade resurser

I [!DNL Policy Service] API, alla policyer och marknadsföringsåtgärder kallas antingen `core` eller `custom` resurser.

`core` är de som definieras och bibehålls av Adobe, medan `custom` är resurser som skapats och underhålls av organisationen och därför är unika och synliga enbart för organisationen. Listans- och uppslagsåtgärder (`GET`) är de enda åtgärder som tillåts på `core` resurser, medan åtgärder för listning, sökning och uppdatering (`POST`, `PUT`, `PATCH`och `DELETE`) finns för `custom` resurser.

## Nästa steg

Välj en av de tillgängliga slutpunktsguiderna för att börja ringa anrop med hjälp av API:t för principtjänsten.
