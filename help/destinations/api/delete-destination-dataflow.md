---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;API;api;delete;ta bort måldata
solution: Experience Platform
title: Ta bort ett måldataflöde med API:t för Flow Service
type: Tutorial
description: Lär dig hur du tar bort dataflöden till batchmål och direktuppspelningsmål med API:t för Flow Service.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Ta bort ett måldataflöde med API:t för Flow Service

Du kan ta bort dataflöden som innehåller fel eller har blivit föråldrade med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

I den här självstudiekursen beskrivs stegen för att ta bort dataflöden till både batch- och direktuppspelningsmål med [!DNL Flow Service].

## Komma igång {#get-started}

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har ett giltigt flödes-ID väljer du önskat mål på menyn [målkatalog](../catalog/overview.md) och följa de steg som beskrivs nedan för att [ansluta till målet](../ui/connect-destination.md) och [aktivera data](../ui/activation-overview.md) innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ta bort ett dataflöde med [!DNL Flow Service] API.

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om konventionerna som används i dokumentationen för exempel-API-anrop finns i avsnittet om [läsa exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i [!DNL Experience Platform] felsökningsguide.

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att ringa [!DNL Platform] API:er måste du först slutföra [självstudiekurs om autentisering](https://www.adobe.com/go/platform-api-authentication-en). När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive sådana som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla förfrågningar till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om `x-sandbox-name` ingen rubrik har angetts, begäranden har lösts under `prod` sandlåda.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Ta bort ett måldataflöde {#delete-destination-dataflow}

Med ett befintligt flödes-ID kan du ta bort ett måldataflöde genom att göra en DELETE-begäran till [!DNL Flow Service] API.

**API-format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för måldataflödet som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) i dataflödet. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudien följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du använt [!DNL Flow Service] API för att ta bort ett befintligt dataflöde till ett mål.

Anvisningar om hur du utför dessa åtgärder med användargränssnittet finns i självstudiekursen om [ta bort dataflöden i användargränssnittet](../ui/delete-destinations.md).

Nu kan du fortsätta och [ta bort destinationskonton](/help/destinations/api/delete-destination-account.md) med [!DNL Flow Service] API.
