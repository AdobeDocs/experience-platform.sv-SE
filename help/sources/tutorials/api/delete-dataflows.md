---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;API;api;delete;delete dataflod
solution: Experience Platform
title: Ta bort ett dataflöde med API:t för flödestjänsten
type: Tutorial
description: Lär dig hur du tar bort batch- och direktuppspelade dataflöden med API:t för Flow Service.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Ta bort ett dataflöde med API:t för Flow Service

Du kan ta bort batch- och direktuppspelade dataflöden som innehåller fel eller har blivit föråldrade med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

I den här självstudiekursen beskrivs stegen för att ta bort dataflöden som skapats med både batch- och direktuppspelningskällor med [!DNL Flow Service].

## Komma igång

Den här självstudiekursen kräver att du har ett giltigt flödes-ID. Om du inte har ett giltigt flödes-ID väljer du den önskade anslutningen på menyn [källöversikt](../../home.md) och följ instruktionerna innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Ta bort ett dataflöde

Med ett befintligt flödes-ID kan du ta bort ett dataflöde genom att göra en DELETE-begäran till [!DNL Flow Service] API.

**API-format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{FLOW_ID}` | Unika `id` värdet för det dataflöde som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext. Du kan bekräfta borttagningen genom att försöka utföra en sökbegäran (GET) i dataflödet. API:t returnerar ett HTTP 404-fel (Hittades inte) som anger att dataflödet har tagits bort.

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!DNL Flow Service] API för att ta bort ett befintligt dataflöde.

Anvisningar om hur du utför dessa åtgärder med användargränssnittet finns i självstudiekursen om [ta bort dataflöden i användargränssnittet](../../tutorials/ui/delete.md)
