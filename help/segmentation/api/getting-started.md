---
keywords: Experience Platform;hem;populära ämnen;segmentering;Segmentering;Segmenteringstjänst;api;
solution: Experience Platform
title: Utvecklarhandbok för segmenteringstjänst
topic: developer guide
description: Följande dokumentation innehåller ytterligare information som du behöver känna till för att kunna arbeta med segmenterings-API:t.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Komma igång med [!DNL Segmentation Service] {#getting-started}

Med Adobe Experience Platform [!DNL Segmentation Service] kan du skapa segment och generera målgrupper i Adobe Experience Platform utifrån dina [!DNL Real-time Customer Profile]-data.

Utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform]-tjänster som används med [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Gör att ni kan skapa målgruppssegment utifrån  [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Sandlådor](../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med API:t [!DNL Segmentation].

## Läser exempel-API-anrop

API-dokumentationen för [!DNL Segmentation Service] innehåller exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering för att kunna anropa [!DNL Platform] slutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop enligt nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på sandlådan där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform] finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

## Nästa steg

Om du vill ringa anrop med API:t [!DNL Segmentation Service] väljer du en av de tillgängliga slutpunktsguiderna antingen med hjälp av den vänstra navigeringen eller i översikten till [utvecklarhandboken](./overview.md)