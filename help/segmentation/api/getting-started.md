---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Utvecklarhandbok för segmenteringstjänst
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Getting started with [!DNL Segmentation Service] {#getting-started}

Med Adobe Experience Platform [!DNL Segmentation Service] kan ni skapa segment och generera målgrupper i Adobe Experience Platform utifrån era [!DNL Real-time Customer Profile] data.

Utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som används [!DNL Segmentation Service].

- [[!DNL-segmentering]](../home.md): Gör att ni kan skapa målgruppssegment utifrån [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna arbeta med [!DNL Segmentation] API:t.

## Läser exempel-API-anrop

API-dokumentationen innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. [!DNL Segmentation Service] Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

## Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa [!DNL Platform] slutpunkter. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform]finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

## Nästa steg

Om du vill ringa anrop med [!DNL Segmentation Service] API:t väljer du en av de tillgängliga slutpunktsguiderna med hjälp av den vänstra navigeringen eller i översikten för [utvecklarhandboken](./overview.md)