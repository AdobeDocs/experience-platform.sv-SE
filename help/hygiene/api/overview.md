---
title: API-guide för datahygien
description: Lär dig att programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# API-guide för datahygien

Med Data Hygiene API kan du programmässigt korrigera eller ta bort dina kunders lagrade personuppgifter i Adobe Experience Platform, samt schemalägga förfallodatum för datauppsättningar. Den här guiden beskriver de nödvändiga stegen för att använda API:t och innehåller länkar till mer slutpunktsspecifik dokumentation.

## Komma igång

Du kan komma åt API:t för datahygien via följande rotsökväg: `https://platform.adobe.io/data/core/hygiene/`

I det här avsnittet nedan beskrivs de grundläggande begrepp som du behöver känna till innan du försöker anropa API:t.

### Samla in värden för obligatoriska rubriker

För att kunna anropa API:t för datahygien måste du först samla in dina autentiseringsuppgifter. Följ [API-autentiseringsguiden](../../landing/api-authentication.md) för att generera värden för vart och ett av de obligatoriska rubrikerna för API:t för datahygien, så som visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

* `Content-Type: application/json`

### Läser exempel-API-anrop

Det här dokumentet innehåller ett exempel-API-anrop som visar hur du formaterar dina begäranden. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/api-guide.md#sample-api) i Komma igång-guiden för Experience Platform-API:er.

## Utgångsdatum för datauppsättning

En datamängds förfallodatum är en tidsfördröjd åtgärd,&quot;ta bort en datamängd&quot;. Genom att skapa en förfallotid för en datauppsättning anger du en framtida tidpunkt då den datauppsättningen ska tas bort. Mer information om hur du schemalägger förfallodatum för datauppsättningar i API finns i [slutpunktshandboken för datauppsättningar](./dataset-expiration.md).

## Posten tas bort

>[!IMPORTANT]
>
>Begäranden om radering av poster är bara tillgängliga för organisationer som har köpt **Adobe Healthcare Shield**.
>
>
>Borttagning av poster ska användas för datarensning, borttagning av anonyma data eller datamängning. De **får inte** användas för förfrågningar om rättigheter för registrerade (efterlevnad) som gäller sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR). Använd [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) i stället för alla kompatibilitetsfall.

Med Data Hygiene API kan du ta bort alla poster som är associerade med en identitet i en eller alla datauppsättningar. Alla uppgifter i datalängden som tar bort identiteter representeras av en konstruktion som kallas arbetsordning. Mer information om hur du arbetar med postborttagningar i API finns i [slutpunktshandboken för arbetsorder](./workorder.md).

## Kvot

Din organisation är begränsad till en fördefinierad månadskvot för varje typ av datalängd, som kan variera beroende på licens. Se [kvotslutpunktshandboken](./quota.md) för mer information om hur du visar den aktuella kvotstatusen för dina datalivscykelprocesser.

## Nästa steg

I den här handboken beskrivs hur du hanterar livscykelbegäranden om data med API-anrop. Information om hur du utför de här åtgärderna i plattformsgränssnittet finns i [användargränssnittsguiden för datalängd](../ui/overview.md).
