---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;api;
solution: Experience Platform
title: Komma igång med segmenteringstjänstens API
topic-legacy: developer guide
description: Följande dokumentation innehåller ytterligare information som du behöver känna till för att kunna arbeta med segmenterings-API:t.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Komma igång med segmenteringstjänstens API {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] kan ni skapa segment och generera målgrupper i Adobe Experience Platform från era [!DNL Real-Time Customer Profile] data.

Utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som används [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Gör att ni kan skapa målgruppssegment utifrån [!DNL Real-Time Customer Profile] data.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med [!DNL Segmentation] API.

## Läser exempel-API-anrop

The [!DNL Segmentation Service] API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en) för att kunna ringa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de rubriker som krävs i [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform], se [översikt över sandlådor](../../sandboxes/home.md).

## Nästa steg

Att ringa samtal med [!DNL Segmentation Service] API: välj en av de tillgängliga slutpunktsstödlinjerna antingen med hjälp av den vänstra navigeringen eller i [utvecklarguide - översikt](./overview.md)
