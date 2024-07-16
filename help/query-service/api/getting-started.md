---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;Fråga
solution: Experience Platform
title: API-guide för frågetjänst
description: Med API:t för frågetjänsten kan utvecklare fråga sina Adobe Experience Platform-data med hjälp av standard-SQL. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# API-guide för [!DNL Query Service]

Den här utvecklarhandboken innehåller steg för att utföra olika åtgärder i API:t för Adobe Experience Platform [!DNL Query Service].

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som används med [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Ger möjlighet att fråga datauppsättningar och hämta de resulterande frågorna som nya datauppsättningar i [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna använda [!DNL Query Service] med API:t.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i den här dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Platform] API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver ett huvud som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådor](../../sandboxes/home.md).

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t [!DNL Query Service]. Följande dokument går igenom de olika API-anropen som du kan göra med API:t [!DNL Query Service]. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

- [Frågor](queries.md)
- [Anslutningsparametrar](connection-parameters.md)
- [Schemalagda frågor](scheduled-queries.md)
- [Körs för schemalagda frågor](runs-scheduled-queries.md)
- [Frågemallar](query-templates.md)
- [Snabbare frågor](./accelerated-queries.md)
- [Aviseringsprenumerationer](./alert-subscriptions.md)

## Nästa steg

Nu när du har lärt dig att ringa anrop med API:t [!DNL Query Service] kan du skapa egna icke-interaktiva frågor. Mer information om hur du skapar frågor finns i [SQL-referenshandboken](../sql/overview.md).
