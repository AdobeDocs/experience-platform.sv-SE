---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;API;api;delete;delete dataflod
solution: Experience Platform
title: Ta bort ett dataflöde med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs stegen för att ta bort batch- och direktuppspelade dataflöden med API:t för Flow Service.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Ta bort ett dataflöde med API:t för Flow Service

Du kan ta bort batch- och direktuppspelade dataflöden som innehåller fel eller har blivit föråldrade med [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

I den här självstudiekursen beskrivs stegen för att ta bort dataflöden som skapats med både batch- och direktuppspelningskällor med [!DNL Flow Service].

## Komma igång

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har ett giltigt flödes-ID väljer du den önskade anslutningen i [källöversikten](../../home.md) och följer instruktionerna innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md):  [!DNL Experience Platform] gör att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av  [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md):  [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda  [!DNL Platform] instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ta bort ett dataflöde med API:t [!DNL Flow Service].

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du är klar med självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop enligt nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i [!DNL Experience Platform], inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Ta bort ett dataflöde

Med ett befintligt flödes-ID kan du ta bort ett dataflöde genom att utföra en DELETE-begäran till API:t [!DNL Flow Service].

**API-format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Det unika `id`-värdet för det dataflöde som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) i dataflödet. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

## Nästa steg

I den här självstudiekursen har du använt API:t [!DNL Flow Service] för att ta bort ett befintligt dataflöde.

Anvisningar om hur du utför dessa åtgärder med användargränssnittet finns i självstudiekursen om att [ta bort dataflöden i användargränssnittet](../../tutorials/ui/delete.md)
