---
keywords: Experience Platform;hem;populära ämnen;katalogtjänst;katalog;katalogtjänst;katalog
solution: Experience Platform
title: API-guide för katalogtjänst
description: Med Catalog Service API kan utvecklare hantera datauppsättningsmetadata i Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# [!DNL Catalog Service] API-guide

[!DNL Catalog Service] är registersystemet för dataplatser och datalinje inom Adobe Experience Platform. [!DNL Catalog] fungerar som ett metadataarkiv eller en katalog där du kan hitta information om dina data i [!DNL Experience Platform]utan att behöva komma åt själva data. Se [[!DNL Catalog] översikt](../home.md) för mer information.

I den här utvecklarhandboken får du hjälp att börja använda [!DNL Catalog] API. Handboken innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med [!DNL Catalog].

## Förutsättningar

[!DNL Catalog] spårar metadata för flera olika typer av resurser och åtgärder i [!DNL Experience Platform]. Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform] tjänster som används för att skapa och hantera dessa resurser:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata.
* [Batchförtäring](../../ingestion/batch-ingestion/overview.md): Hur [!DNL Experience Platform] importerar och lagrar data från datafiler, som CSV och Parquet.
* [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Hur [!DNL Experience Platform] importerar och lagrar data från klient- och serverenheter i realtid.

I följande avsnitt finns ytterligare information som du behöver känna till eller har till hands för att kunna ringa till [!DNL Catalog Service] API.

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

## Samla in värden för obligatoriska rubriker

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform], se [översiktsdokumentation för sandlåda](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Bästa tillvägagångssätt för [!DNL Catalog] API-anrop

Vid GET av begäranden till [!DNL Catalog] API, är det bästa sättet att ta med frågeparametrar i dina förfrågningar för att bara returnera de objekt och egenskaper som du behöver. Ofiltrerade begäranden kan göra att svarsnyttolasterna når över 3 GB, vilket kan göra den totala prestandan långsammare.

Du kan visa specifika objekt genom att ta med deras ID i den begärda sökvägen eller använda frågeparametrar som `properties` och `limit` för att filtrera svaren. Filter kan skickas som rubriker och som frågeparametrar, där de skickas som frågeparametrar har prioritet. Visa dokumentet på [filtrera katalogdata](filter-data.md) för mer information.

Eftersom vissa frågor kan göra API:t mycket belastat har globala begränsningar implementerats på [!DNL Catalog] frågor för att ytterligare stödja bästa praxis.

## Nästa steg

Det här dokumentet innehöll de nödvändiga kunskaperna som krävs för att ringa till [!DNL Catalog] API. Du kan nu gå vidare till exempelsamtalen i den här utvecklarhandboken och följa med i instruktionerna för dessa.

De flesta exemplen i den här handboken använder `/dataSets` slutpunkt, men principerna kan tillämpas på andra slutpunkter inom [!DNL Catalog] (till exempel `/batches` och `/accounts`). Se [API-referens för katalogtjänst](https://www.adobe.io/experience-platform-apis/references/catalog/) för en fullständig lista över alla anrop och åtgärder som är tillgängliga för varje slutpunkt.

Ett stegvis arbetsflöde som visar hur [!DNL Catalog] API:t är involverat i datainmatning, se självstudiekursen om [skapa en datauppsättning](../datasets/create.md).
