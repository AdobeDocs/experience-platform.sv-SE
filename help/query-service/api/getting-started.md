---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Handbok för frågetjänstutvecklare
topic: query templates
description: Den här utvecklarhandboken innehåller steg för att utföra olika åtgärder i Adobe Experience Platform Query Service API.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---


# [!DNL Query Service] utvecklarhandbok

Den här utvecklarhandboken innehåller steg för att utföra olika åtgärder i Adobe Experience Platform [!DNL Query Service] API.

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som används i [!DNL Query Service].

- [!DNL Query Service](../home.md): Ger möjlighet att fråga datauppsättningar och hämta de resulterande frågorna som nya datauppsättningar i [!DNL Experience Platform].
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna använda API [!DNL Query Service] .

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i den här dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Experience Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Platform] API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform]finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till [!DNL Query Service] API:t. Följande dokument går igenom de olika API-anropen som du kan göra med [!DNL Query Service] API:t. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

- [Frågor](queries.md)
- [Anslutningsparametrar](connection-parameters.md)
- [Schemalagda frågor](scheduled-queries.md)
- [Körs för schemalagda frågor](runs-scheduled-queries.md)
- [Frågemallar](query-templates.md)

## Nästa steg

Nu när du har lärt dig att ringa samtal med API:t kan du skapa egna icke-interaktiva frågor. [!DNL Query Service] Mer information om hur du skapar frågor finns i [SQL-referenshandboken](../sql/overview.md).