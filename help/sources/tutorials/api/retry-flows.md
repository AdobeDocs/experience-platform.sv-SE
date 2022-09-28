---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;
title: Försök igen med misslyckade dataflödeskörningar
description: I den här självstudien beskrivs hur du provar misslyckade dataflöden på nytt med API:t för Flow Service
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Försök igen med misslyckade dataflödeskörningar

>[!IMPORTANT]
>
>Stöd för att försöka utföra misslyckade dataflödeskörningar finns för batchkällor. Du kan bara försöka köra dataflödet igen som har misslyckats.

I den här självstudiekursen beskrivs hur du provar misslyckade dataflöden på nytt med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Försök igen med ett misslyckat dataflöde

Om du vill försöka köra ett misslyckat dataflöde igen skickar du en POST till `/runs` slutpunkten när du anger ID:t för körningen av dataflödet och `re-trigger` som en del av frågeparametrarna.

**API-format**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beskrivning |
| --- | --- |
| `{RUN_ID}` | Det körnings-ID som motsvarar dataflödeskörningen som du vill försöka igen. |
| `op` | En åtgärd som avgör vilken åtgärd som ska utföras. Om du vill försöka köra ett misslyckat dataflöde igen måste du ange `re-trigger` som din åtgärd. |

**Begäran**

Följande begäran försöker köra dataflödet igen för körnings-ID `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Svar**

Ett lyckat svar returnerar ett nyligen skapat flödeskörnings-ID och dess motsvarande taggversion.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
