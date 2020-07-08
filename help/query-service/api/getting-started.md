---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbok för frågetjänstutvecklare
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Handbok för frågetjänstutvecklare

Den här utvecklarhandboken innehåller steg för att utföra olika åtgärder i Adobe Experience Platform Query Service API.

## Komma igång

Den här guiden kräver en fungerande förståelse av de olika Adobe Experience Platform-tjänster som används med Query Service.

- [Frågetjänst](../home.md): Ger möjlighet att fråga datauppsättningar och hämta de resulterande frågorna som nya datauppsättningar i Experience Platform.
- [Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
- [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna använda frågetjänsten med API:t.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i den här dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API:er för Experience Platform måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla Platform API-anrop, vilket visas nedan:

- Behörighet: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på den sandlåda där åtgärden ska utföras:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om hur du arbetar med sandlådor i Experience Platform finns i översiktsdokumentationen för [sandlådor](../../sandboxes/home.md).

## Exempel på API-anrop

Nu när du förstår vilka rubriker som ska användas kan du börja ringa anrop till API:t för frågetjänsten. Följande dokument går igenom de olika API-anropen som du kan göra med hjälp av API:t för frågetjänsten. Varje exempelanrop innehåller det allmänna API-formatet, en exempelbegäran med obligatoriska rubriker och ett exempelsvar.

- [Frågor](queries.md)
- [Anslutningsparametrar](connection-parameters.md)
- [Schemalagda frågor](scheduled-queries.md)
- [Körs för schemalagda frågor](runs-scheduled-queries.md)
- [Frågemallar](query-templates.md)

## Nästa steg

Nu när du har lärt dig hur du ringer samtal med hjälp av API:t för frågetjänsten kan du skapa egna icke-interaktiva frågor. Mer information om hur du skapar frågor finns i [SQL-referenshandboken](../sql/overview.md).