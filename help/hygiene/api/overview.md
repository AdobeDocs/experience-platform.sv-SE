---
title: API-guide för datahygien
description: Lär dig att programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# API-guide för datahygien

Med Data Hygiene API kan du programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform, samt schemalägga förfallodatum för datauppsättningar. Den här guiden beskriver de nödvändiga stegen för att använda API:t och innehåller länkar till mer slutpunktsspecifik dokumentation.

## Komma igång

Du kommer åt API:t för datahygien via följande rotsökväg: `https://platform.adobe.io/data/core/hygiene/`

I det här avsnittet nedan beskrivs de grundläggande begrepp som du behöver känna till innan du försöker anropa API:t.

### Samla in värden för obligatoriska rubriker

För att kunna anropa API:t för datahygien måste du först samla in dina autentiseringsuppgifter. Följ [API-autentiseringsguide](../../landing/api-authentication.md) för att generera värden för var och en av de rubriker som krävs för API:t för datahygien, enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

### Läser exempel-API-anrop

Det här dokumentet innehåller ett exempel-API-anrop som visar hur du formaterar dina begäranden. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/api-guide.md#sample-api) i guiden Komma igång för Experience Platform API:er.

## Utgångsdatum för datauppsättning

En datamängds förfallodatum är en tidsfördröjd åtgärd,&quot;ta bort en datamängd&quot;. Genom att skapa en förfallotid för en datauppsättning anger du en framtida tidpunkt då den datauppsättningen ska tas bort. Se [Slutpunktshandbok för datauppsättningens förfallodatum](./dataset-expiration.md) om du vill ha mer information om schemaläggning av datauppsättningens förfallodatum i API:t.

## Posten tas bort

>[!IMPORTANT]
>
>Begäran om att radera poster är bara tillgänglig för organisationer som har köpt **Adobe Healthcare Shield**.
>
>
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De är **not** som ska användas för förfrågningar om registrerade rättigheter (överensstämmelse) som rör sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). För all användning av regelefterlevnad [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället.

Med Data Hygiene API kan du ta bort alla poster som är associerade med en identitet i en eller alla datauppsättningar. Alla uppgifter i datalängden som tar bort identiteter representeras av en konstruktion som kallas arbetsordning. Se [slutpunktsguide för arbetsorder](./workorder.md) om du vill ha information om hur du arbetar med postborttagningar i API:t.

## Kvot

Din organisation är begränsad till en fördefinierad månadskvot för varje typ av datalängd, som kan variera beroende på licens. Se [kvotslutpunktshandbok](./quota.md) om du vill ha mer information om hur du ser den aktuella kvotstatusen för datalivscykelprocesserna.

## Nästa steg

I den här handboken beskrivs hur du hanterar livscykelbegäranden om data med API-anrop. Information om hur du utför dessa åtgärder i plattformsgränssnittet finns i [användargränssnittshandbok för datalängd](../ui/overview.md).
