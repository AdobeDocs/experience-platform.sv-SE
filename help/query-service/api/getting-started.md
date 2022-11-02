---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Fråga
solution: Experience Platform
title: API-guide för frågetjänst
topic-legacy: query templates
description: Med API:t för frågetjänsten kan utvecklare fråga sina Adobe Experience Platform-data med hjälp av standard-SQL. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 9f458a327c0b72a5984161f13f02d09b7a2e610e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# [!DNL Query Service] API-guide

Den här utvecklarhandboken innehåller steg för att utföra olika åtgärder i Adobe Experience Platform [!DNL Query Service] API.

## Komma igång

Den här guiden kräver en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används för [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Ger möjlighet att fråga datauppsättningar och hämta de resulterande frågorna som nya datauppsättningar i [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna använda [!DNL Query Service] med API:t.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i den här dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker

För att ringa [!DNL Experience Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Platform] API-anrop enligt nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform], se [översikt över sandlådor](../../sandboxes/home.md).

## Exempel på API-anrop

Nu när du förstår vilka rubriker du ska använda kan du börja ringa till [!DNL Query Service] API. Följande dokument går igenom de olika API-anropen som du kan göra med [!DNL Query Service] API. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

- [Frågor](queries.md)
- [Anslutningsparametrar](connection-parameters.md)
- [Schemalagda frågor](scheduled-queries.md)
- [Körs för schemalagda frågor](runs-scheduled-queries.md)
- [Frågemallar](query-templates.md)
- [Snabbare frågor](./accelerated-queries.md)
- [Aviseringsprenumerationer](./alert-subscriptions.md)

## Nästa steg

Nu när du har lärt dig hur man ringer med [!DNL Query Service] API kan du skapa egna icke-interaktiva frågor. Mer information om hur du skapar frågor finns i [SQL-referenshandbok](../sql/overview.md).
