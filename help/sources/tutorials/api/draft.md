---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;
title: Utkastdataflöden med API:t för flödestjänsten
description: Lär dig hur du ställer in dataflöden i ett utkasttillstånd med API:t för Flow Service.
badge: label="New Feature" type="Positive"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Utkastdataflöden med API:t för Flow Service

Spara dina dataflöden som utkast när du använder API:t för Flow Service genom att ange `mode=draft` frågeparameter när flödet skapas. Utkasten kan uppdateras senare med ny information och sedan publiceras när de är klara. I den här självstudien beskrivs stegen för hur du ställer in dataflöden i ett utkasttillstånd med API:t för Flow Service.

## Komma igång

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Förutsättningar

Den här självstudien kräver att du redan har genererat de resurser som behövs för att skapa ett dataflöde. Detta inkluderar följande:

* En autentiserad basanslutning
* En källanslutning
* Ett mål-XDM-schema
* En måldatamängd
* En målanslutning
* En mappning

Om du ännu inte har dessa värden väljer du en källa från [katalogen i källorna - översikt](../../home.md). Följ sedan instruktionerna från den angivna källan för att generera de resurser som krävs för att skapa ett dataflöde.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Ange ett dataflöde till utkastläge

I följande avsnitt beskrivs processen att ställa in ett dataflöde som ett utkast, uppdatera dataflödet, publicera dataflödet och slutligen ta bort dataflödet.

### Utforma ett dataflöde

Om du vill ange ett dataflöde som ett utkast gör du en POST-förfrågan till `/flows` slutpunkt när du lägger till `mode=draft` som en frågeparameter. På så sätt kan du skapa ett dataflöde och spara det som ett utkast.

**API-format**

```http
POST /flows?mode=draft
```

| Parameter | Beskrivning |
| --- | --- |
| `mode` | En frågeparameter som användaren anger och som avgör dataflödets tillstånd. Ange ett dataflöde som ett utkast `mode` till `draft`. |

**Begäran**

Följande begäran skapar ett utkast till dataflöde.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Svar**

Ett godkänt svar returnerar `id` och motsvarande `etag` av dataflödet.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Uppdatera ett dataflöde

Om du vill uppdatera utkastet gör du en PATCH-förfrågan till `/flows` slutpunkten när du anger ID:t för det dataflöde som du vill uppdatera. Under det här steget måste du även ange en `If-Match` rubrikparameter, som motsvarar `etag` av det dataflöde som du vill uppdatera.

**API-format**

```http
PATCH /flows/{FLOW_ID}
```

**Begäran**

Följande begäranden lägger till mappningsomvandlingar i det utkast som används i dataflödet.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Svar**

Ett lyckat svar returnerar ditt flödes-ID och `etag`. Du kan göra en GET-förfrågan till `/flows` slutpunkt när ditt flödes-ID anges.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publicera ett dataflöde

När utkastet är klart för publicering skickar du en POST till `/flows` slutpunkten när du anger ID:t för det dataflöde du vill publicera samt en åtgärd för publicering.

**API-format**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beskrivning |
| --- | --- |
| `op` | En åtgärd som uppdaterar tillståndet för det efterfrågade dataflödet. Om du vill publicera ett utkast anger du `op` till `publish`. |

**Begäran**

Följande begäran publicerar ditt utkast till dataflöde.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett godkänt svar returnerar ID:t och motsvarande `etag` av dataflödet.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Ta bort ett dataflöde

Om du vill ta bort dataflödet skickar du en DELETE-förfrågan till `/flows` slutpunkten när du anger ID:t för det dataflöde som du vill ta bort. Detaljerade anvisningar om hur du tar bort ett dataflöde med API:t för Flow Service finns i handboken på [ta bort ett dataflöde i API](./delete-dataflows.md).
