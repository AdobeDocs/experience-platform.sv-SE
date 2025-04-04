---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;API;api;delete;delete destinationsdataflöden
solution: Experience Platform
title: Ta bort ett måldataflöde med API:t för Flow Service
type: Tutorial
description: Lär dig hur du tar bort dataflöden till batchmål och direktuppspelningsmål med API:t för Flow Service.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 4%

---

# Ta bort ett måldataflöde med API:t för Flow Service

Du kan ta bort dataflöden som innehåller fel eller som har blivit föråldrade med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

I den här självstudien beskrivs stegen för att ta bort dataflöden till både batch- och direktuppspelningsmål med hjälp av [!DNL Flow Service].

## Komma igång {#get-started}

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har något giltigt flöde-ID väljer du önskat mål i [målkatalogen](../catalog/overview.md) och följer instruktionerna som beskrivs för att [ansluta till målet](../ui/connect-destination.md) och [aktivera data](../ui/activation-overview.md) innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Destinationer](../home.md): [!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.
* [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ta bort ett dataflöde med API:t [!DNL Flow Service].

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker {#gather-values-for-required-headers}

För att kunna anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Om rubriken `x-sandbox-name` inte anges löses förfrågningar under sandlådan `prod`.

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver en extra medietypsrubrik:

* `Content-Type: application/json`

## Ta bort ett måldataflöde {#delete-destination-dataflow}

Med ett befintligt flödes-ID kan du ta bort ett måldataflöde genom att utföra en DELETE-begäran till [!DNL Flow Service]-API:t.

**API-format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Det unika `id`-värdet för måldataflödet som du vill ta bort. |

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

Ett lyckat svar returnerar HTTP-status 202 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET)-begäran i dataflödet. API returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

## API-felhantering {#api-error-handling}

API-slutpunkterna i den här självstudien följer de allmänna felmeddelandeprinciperna för Experience Platform API. Mer information om hur du tolkar felsvar finns i [API-statuskoder](/help/landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](/help/landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du använt API:t [!DNL Flow Service] för att ta bort ett befintligt dataflöde till ett mål.

Anvisningar om hur du utför dessa åtgärder med användargränssnittet finns i självstudiekursen [Ta bort dataflöden i användargränssnittet](../ui/delete-destinations.md).

Du kan nu fortsätta och [ta bort målkonton](/help/destinations/api/delete-destination-account.md) med API:t [!DNL Flow Service].
