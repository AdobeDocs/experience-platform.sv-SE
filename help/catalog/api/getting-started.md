---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;Catalog
solution: Experience Platform
title: Utvecklarhandbok för katalogtjänst
topic: developer guide
description: Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda Catalog API. Handboken innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med hjälp av Katalog.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# [!DNL Catalog Service] utvecklarhandbok

[!DNL Catalog Service] är registersystemet för dataplatser och datalinje inom Adobe Experience Platform. [!DNL Catalog] fungerar som ett metadataarkiv eller en&quot;katalog&quot; där du kan hitta information om dina data inifrån [!DNL Experience Platform]utan att behöva komma åt själva data. Mer information finns i [Katalogöversikt](../home.md) .

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda [!DNL Catalog] API:t. Handboken innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med [!DNL Catalog].

## Förutsättningar

[!DNL Catalog] spårar metadata för flera olika typer av resurser och åtgärder i [!DNL Experience Platform]. Utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som är förknippade med att skapa och hantera dessa resurser:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.
* [Batchförtäring](../../ingestion/batch-ingestion/overview.md): Så här [!DNL Experience Platform] importerar och lagrar du data från datafiler, som CSV och Parquet.
* [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Hur data [!DNL Experience Platform] importeras och lagras från klient- och serverenheter i realtid.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa [!DNL Catalog Service] API:t.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguiden.

## Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till API: [!DNL Platform] er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla förfrågningar till API: [!DNL Platform] er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform]finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Bästa tillvägagångssätt för [!DNL Catalog] API-anrop

När du gör GET-begäranden till API:t är det bäst att ta med frågeparametrar i dina begäranden för att bara returnera de objekt och egenskaper som du behöver. [!DNL Catalog] Ofiltrerade begäranden kan göra att svarsnyttolasterna når över 3 GB, vilket kan göra den totala prestandan långsammare.

Du kan visa specifika objekt genom att ta med deras ID i den begärda sökvägen eller använda frågeparametrar som `properties` och `limit` för att filtrera svar. Filter kan skickas som rubriker och som frågeparametrar, där de skickas som frågeparametrar har prioritet. Mer information finns i dokumentet om [filtrering av katalogdata](filter-data.md) .

Eftersom vissa frågor kan belasta API:t avsevärt, har globala begränsningar implementerats på frågor för att ytterligare stödja bästa praxis. [!DNL Catalog]

## Nästa steg

Det här dokumentet innehöll den nödvändiga kunskapen som krävs för att ringa anrop till [!DNL Catalog] API:t. Du kan nu gå vidare till exempelsamtalen i den här utvecklarhandboken och följa med i instruktionerna för dessa.

I de flesta av exemplen i den här handboken används `/dataSets` slutpunkten, men principerna kan tillämpas på andra slutpunkter inom [!DNL Catalog] (till exempel `/batches` och `/accounts`). En fullständig lista över alla anrop och åtgärder som är tillgängliga för varje slutpunkt finns i API-referensen [för](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) katalogtjänsten.

Ett stegvis arbetsflöde som demonstrerar hur API:t [!DNL Catalog] används för datainmatning finns i självstudiekursen om hur du [skapar en datauppsättning](../datasets/create.md).
