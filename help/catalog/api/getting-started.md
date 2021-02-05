---
keywords: Experience Platform;hem;populära ämnen;katalogtjänst;katalog;katalogtjänst;katalog
solution: Experience Platform
title: API-guide för katalogtjänst
topic: developer guide
description: Med Catalog Service API kan utvecklare hantera datauppsättningsmetadata i Adobe Experience Platform. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# [!DNL Catalog Service] API-guide

[!DNL Catalog Service] är registersystemet för dataplatser och datalinje inom Adobe Experience Platform. [!DNL Catalog] fungerar som ett metadataarkiv eller en&quot;katalog&quot; där du kan hitta information om dina data inifrån  [!DNL Experience Platform]utan att behöva komma åt själva data. Mer information finns i [[!DNL Catalog] översikten](../home.md).

Den här utvecklarhandboken innehåller steg som hjälper dig att börja använda API:t [!DNL Catalog]. Guiden innehåller sedan exempel på API-anrop för att utföra nyckelåtgärder med [!DNL Catalog].

## Förutsättningar

[!DNL Catalog] spårar metadata för flera olika typer av resurser och åtgärder i  [!DNL Experience Platform]. Den här utvecklarhandboken kräver en fungerande förståelse av de olika [!DNL Experience Platform]-tjänster som används för att skapa och hantera dessa resurser:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.
* [Batchförtäring](../../ingestion/batch-ingestion/overview.md): Hur  [!DNL Experience Platform] importerar och lagrar data från datafiler, som CSV och Parquet.
* [Direktinmatning](../../ingestion/streaming-ingestion/overview.md): Hur  [!DNL Experience Platform] inhämtar och lagrar data från klient- och serverenheter i realtid.

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa API:t [!DNL Catalog Service].

## Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

## Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* Innehållstyp: application/json

## Bästa tillvägagångssätt för [!DNL Catalog] API-anrop

När du gör GET-begäranden till API:t [!DNL Catalog] är det bäst att ta med frågeparametrar i dina begäranden för att bara returnera de objekt och egenskaper som du behöver. Ofiltrerade begäranden kan göra att svarsnyttolasterna når över 3 GB, vilket kan göra den totala prestandan långsammare.

Du kan visa specifika objekt genom att ta med deras ID i den begärda sökvägen eller använda frågeparametrar som `properties` och `limit` för att filtrera svar. Filter kan skickas som rubriker och som frågeparametrar, där de skickas som frågeparametrar har prioritet. Mer information finns i dokumentet om [filtrering av katalogdata](filter-data.md).

Eftersom vissa frågor kan innebära en stor belastning på API:t har globala begränsningar implementerats på [!DNL Catalog]-frågor för att ytterligare stödja bästa praxis.

## Nästa steg

Det här dokumentet innehöll den nödvändiga kunskapen som krävs för att anropa API:t [!DNL Catalog]. Du kan nu gå vidare till exempelsamtalen i den här utvecklarhandboken och följa med i instruktionerna för dessa.

De flesta av exemplen i den här handboken använder slutpunkten `/dataSets`, men principerna kan tillämpas på andra slutpunkter inom [!DNL Catalog] (till exempel `/batches` och `/accounts`). Se [API-referens för katalogtjänst](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) för en fullständig lista över alla anrop och åtgärder som är tillgängliga för varje slutpunkt.

Ett steg-för-steg-arbetsflöde som demonstrerar hur API:t [!DNL Catalog] är involverat i datainmatning finns i självstudiekursen om att [skapa en datauppsättning](../datasets/create.md).
