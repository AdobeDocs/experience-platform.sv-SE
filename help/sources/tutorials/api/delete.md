---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;ta bort konton;ta bort;api
solution: Experience Platform
title: Ta bort ett konto med API:t för Flow Service
type: Tutorial
description: Lär dig hur du tar bort ett konto med API:t för Flow Service.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Ta bort ett konto med API:t för Flow Service

Du kan ta bort källkonton som innehåller fel eller har blivit inaktuella med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

I följande självstudiekurs finns anvisningar om hur du tar bort ett konto med API:t.

## Komma igång

Den här självstudiekursen kräver att du har ett giltigt anslutnings-ID. Om du inte har något giltigt anslutnings-ID väljer du den önskade anslutningen på menyn [källöversikt](../../home.md) och följ instruktionerna innan du provar den här självstudiekursen.

Den här självstudiekursen kräver även att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Ta bort konto

>[!TIP]
>
>Innan du tar bort källkontot måste du först ta bort alla befintliga dataflöden som är kopplade till källkontot. Om du vill ta bort befintliga dataflöden kan du läsa självstudiekursen om [ta bort källfilsdataflöden](./delete-dataflows.md).

Om du vill ta bort ett konto gör du en DELETE-förfrågan till [!DNL Flow Service] API:t anger det basanslutnings-ID som motsvarar kontot som du vill ta bort.

**API-format**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Basanslutnings-ID för det källkonto som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och en tom brödtext.

Du kan bekräfta borttagningen genom att försöka utföra en sökning (GET) på anslutningen.

## Nästa steg

Genom att följa den här självstudiekursen har du använt [!DNL Flow Service] API för att ta bort befintliga konton.

Anvisningar om hur du utför dessa åtgärder med användargränssnittet finns i självstudiekursen om [ta bort konton i användargränssnittet](../../tutorials/ui/delete-accounts.md).
