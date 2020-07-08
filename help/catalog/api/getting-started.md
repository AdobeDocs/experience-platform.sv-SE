---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för katalogtjänst
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Utvecklarhandbok för katalogtjänst

Katalogtjänsten är ett system för registrering av dataplatser och -länkar inom Adobe Experience Platform. Katalogen fungerar som ett metadataarkiv eller en&quot;katalog&quot; där du kan hitta information om dina data i Experience Platform, utan att behöva komma åt själva data. Mer information finns i [Katalogöversikt](../home.md) .

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda Catalog API. Handboken innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med hjälp av Katalog.

## Förutsättningar

Katalogen spårar metadata för flera olika typer av resurser och åtgärder i Experience Platform. Utvecklarhandboken kräver en fungerande förståelse för de olika Experience Platform-tjänster som är kopplade till att skapa och hantera dessa resurser:

* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.
* [Batchförtäring](../../ingestion/batch-ingestion/overview.md): Så här importerar och lagrar Experience Platform data från datafiler, som CSV och Parquet.
* [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Så här importerar och lagrar Experience Platform data från klient- och serverenheter i realtid.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna ringa anrop till katalogtjänstens API.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Bästa tillvägagångssätt för Catalog API-anrop

När du gör GET-begäranden till katalog-API:t är det bäst att ta med frågeparametrar i dina begäranden för att bara returnera de objekt och egenskaper som du behöver. Ofiltrerade begäranden kan göra att svarsnyttolasterna når över 3 GB, vilket kan göra den totala prestandan långsammare.

Du kan visa specifika objekt genom att ta med deras ID i den begärda sökvägen eller använda frågeparametrar som `properties` och `limit` för att filtrera svar. Filter kan skickas som rubriker och som frågeparametrar, där de skickas som frågeparametrar har prioritet. Mer information finns i dokumentet om [filtrering av katalogdata](filter-data.md) .

Eftersom vissa frågor kan innebära en stor belastning på API:t har globala begränsningar implementerats på katalogfrågor för att ytterligare stödja bästa praxis.

## Nästa steg

Det här dokumentet innehöll den nödvändiga kunskapen som krävs för att anropa Catalog API. Du kan nu gå vidare till exempelsamtalen i den här utvecklarhandboken och följa med i instruktionerna för dessa.

I de flesta av exemplen i den här handboken används `/dataSets` slutpunkten, men principerna kan tillämpas på andra slutpunkter i katalogen (till exempel `/batches` och `/accounts`). En fullständig lista över alla anrop och åtgärder som är tillgängliga för varje slutpunkt finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) katalogtjänsten.

Ett steg-för-steg-arbetsflöde som demonstrerar hur katalog-API:t används vid dataöverföring finns i självstudiekursen om hur du [skapar en datauppsättning](../datasets/create.md).
