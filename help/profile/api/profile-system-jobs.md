---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för profilsystemjobb
type: Documentation
description: Med Adobe Experience Platform kan du ta bort en datauppsättning eller batch från profilbutiken för att ta bort kundprofildata i realtid som inte längre behövs eller som har lagts till av misstag. Detta kräver att du använder profil-API:t för att skapa ett profilsystemjobb eller för att ta bort en begäran.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---

# Slutpunkt för profilsystemjobb (Delete-begäranden)

>[!IMPORTANT]
>
>Följande slutpunkter kan skilja sig åt mellan implementeringar av Adobe Experience Platform som körs på Microsoft Azure och Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](https://experienceleague.adobe.com/sv/docs/experience-platform/landing/multi-cloud).

Med Adobe Experience Platform kan ni importera data från flera olika källor och skapa robusta profiler för enskilda kunder. Data som inhämtas till [!DNL Experience Platform] lagras i [!DNL Data Lake], och om datauppsättningarna har aktiverats för profilen lagras även dessa data i datalagret [!DNL Real-Time Customer Profile]. Ibland kan det vara nödvändigt att ta bort profildata som är kopplade till en datauppsättning från profilarkivet för att ta bort data som inte längre behövs eller som har lagts till av misstag. Detta kräver att [!DNL Real-Time Customer Profile]-API:t används för att skapa ett [!DNL Profile]-systemjobb eller en&quot;borttagningsbegäran&quot;.

>[!NOTE]
>
>Om du försöker ta bort datauppsättningar eller grupper från [!DNL Data Lake] kan du gå till [Katalogtjänstöversikten](../../catalog/home.md) om du vill ha mer information.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett Experience Platform-API.

## Visa borttagningsbegäranden {#view}

En borttagningsbegäran är en långvarig, asynkron process, vilket innebär att din organisation kan köra flera borttagningsbegäranden samtidigt. Om du vill visa alla borttagningsbegäranden som din organisation för närvarande kör kan du utföra en GET-begäran till slutpunkten `/system/jobs`.

Du kan också använda valfria frågeparametrar för att filtrera listan med borttagningsbegäranden som returneras i svaret. Om du vill använda flera parametrar avgränsar du varje parameter med ett et-tecken (`&`).

**API-format**

>[!AVAILABILITY]
>
>Följande frågeparametrar är **endast** tillgängliga när du använder Experience Platform på Microsoft Azure.
>
>När du använder den här slutpunkten på AWS returneras de första 100 systemjobben i fallande ordning, baserat på när de skapades.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning | Exempel |
| --------- | ----------- | ------- |
| `start` | Förskjut den returnerade resultatsidan enligt skapandetiden för begäran. | `start=4` |
| `limit` | Begränsa antalet returnerade resultat. | `limit=10` |
| `page` | Returnera en specifik resultatsida enligt skapandetiden för begäran. | `page=2` |
| `sort` | Sortera resultat efter ett specifikt fält i stigande (`asc`) eller fallande (`desc`) ordning. Sorteringsparametern fungerar inte när flera resultatsidor returneras. | `sort=batchId:asc` |

**Begäran**

>[!IMPORTANT]
>
>Följande begäran skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Ett exempel på en förfrågan om att visa systemjobben.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Du **måste** använda begärandehuvudet `x-sandbox-id` i stället för begärandehuvudet `x-sandbox-name` när du använder den här slutpunkten med AWS.

+++ Ett exempel på en förfrågan om att visa systemjobben.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Svar**

>[!IMPORTANT]
>
>Följande svar skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Ett lyckat svar innehåller en &quot;child&quot;-array med ett objekt för varje borttagningsbegäran som innehåller information om begäran.

+++ Ett godkänt svar för att visa borttagningsbegäranden

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `_page.count` | Totalt antal begäranden. Svaret har trunkerats för utrymme. |
| `_page.next` | Om det finns ytterligare en resultatsida kan du visa nästa resultatsida genom att ersätta ID-värdet i en [uppslagsbegäran](#view-a-specific-delete-request) med det angivna `"next"`-värdet. |
| `jobType` | Den typ av jobb som skapas. I det här fallet returneras alltid `"DELETE"`. |
| `status` | Status för borttagningsbegäran. Möjliga värden är `"NEW"`, `"PROCESSING"`, `"COMPLETED"` och `"ERROR"`. |
| `metrics` | Ett objekt som innehåller antalet poster som har bearbetats (`"recordsProcessed"`) och tiden i sekunder som begäran har bearbetats, eller hur lång tid det tog att slutföra begäran (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Ett lyckat svar returnerar en array som innehåller ett objekt för varje systembegäran.

+++ Ett godkänt svar för att visa systemförfrågningar

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `requestId` | ID:t för systemjobbet. |
| `requestType` | Systemjobbets typ. Möjliga värden är `BACKFILL_TTL`, `DELETE_EE_BATCH` och `TRUNCATE_DATASET`. |
| `status` | Systemjobbets status. Möjliga värden är `NEW`, `SUCCESS`, `ERROR`, `FAILED` och `IN-PROGRESS`. |
| `properties` | Ett objekt som innehåller batch- och/eller datauppsättnings-ID för systemjobbet. |

+++

>[!ENDTABS]

## Skapa en borttagningsbegäran {#create-a-delete-request}

Initieringen av en ny borttagningsbegäran görs via en POST-begäran till `/systems/jobs`-slutpunkten, där ID:t för datauppsättningen eller batchen som ska tas bort anges i förfrågningens innehåll.

### Ta bort en datauppsättning och associerade profildata

Om du vill ta bort en datauppsättning och alla profildata som är associerade med datauppsättningen från profilarkivet måste datauppsättnings-ID:t inkluderas i POST-begärans innehåll. Den här åtgärden tar bort ALLA data för en viss datauppsättning. Med [!DNL Experience Platform] kan du ta bort datauppsättningar baserat på scheman för både post- och tidsserier.

**API-format**

```http
POST /system/jobs
```

**Begäran**

>[!IMPORTANT]
>
>Följande begäran skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ En exempelbegäran om att ta bort en datauppsättning.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Egenskap | Beskrivning |
| -------- | ----------- |
| `dataSetId` | ID:t för den datauppsättning som du vill ta bort. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Du **måste** använda begärandehuvudet `x-sandbox-id` i stället för begärandehuvudet `x-sandbox-name` när du använder den här slutpunkten med AWS.

+++ En exempelbegäran om att ta bort en datauppsättning.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Egenskap | Beskrivning |
| -------- | ----------- |
| `dataSetId` | ID:t för den datauppsättning som du vill ta bort. |

>[!ENDTABS]

**Svar**

>[!IMPORTANT]
>
>Följande svar skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Ett lyckat svar returnerar information om den nyligen skapade borttagningsbegäran, inklusive ett unikt, systemgenererat, skrivskyddat ID för begäran. Detta kan användas för att slå upp begäran och kontrollera dess status. `status` för begäran när den skapas är `"NEW"` tills bearbetningen börjar. `dataSetId` i svaret ska matcha `dataSetId` som skickats i begäran.

+++ Ett svar på begäran om borttagning.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Det unika, systemgenererade skrivskyddade ID:t för borttagningsbegäran. |
| `dataSetId` | Datamängdens ID, enligt POST-begäran. |

+++

>[!TAB Amazon Web Services (AWS)]

Ett lyckat svar returnerar information om den nyligen skapade systembegäran.

+++ Ett svar på begäran om borttagning.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `requestId` | ID:t för systemjobbet. |
| `requestType` | Systemjobbets typ. Möjliga värden är `BACKFILL_TTL`, `DELETE_EE_BATCH` och `TRUNCATE_DATASET`. |
| `status` | Systemjobbets status. Möjliga värden är `NEW`, `SUCCESS`, `ERROR`, `FAILED` och `IN-PROGRESS`. |
| `properties` | Ett objekt som innehåller batch- och/eller datauppsättnings-ID för systemjobbet. |

+++

>[!ENDTABS]

### Ta bort en grupp

Om du vill ta bort en batch måste batch-ID:t inkluderas i BOKFÖR-begäran. Observera att du inte kan ta bort grupper för datauppsättningar baserat på postscheman. Endast batchar för datauppsättningar som baseras på tidsseriescheman kan tas bort.

>[!NOTE]
>
> Orsaken till att du inte kan ta bort batchar för datauppsättningar baserade på postscheman är att datauppsättningsbatchar skriver över tidigare poster och därför inte kan ångras eller tas bort. Det enda sättet att ta bort effekten av felaktiga batchar för datauppsättningar som baseras på postscheman är att importera om gruppen med rätt data för att skriva över felaktiga poster.

Mer information om post- och tidsseriebeteende finns i avsnittet [om XDM-databeteenden](../../xdm/home.md#data-behaviors) i översikten [!DNL XDM System].

**API-format**

```http
POST /system/jobs
```

**Begäran**

>[!IMPORTANT]
>
>Följande begäran skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ En exempelbegäran om att ta bort en sats.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Egenskap | Beskrivning |
| -------- | ----------- |
| `datasetId` | ID:t för datauppsättningen för den grupp som du vill ta bort. |
| `batchId` | ID:t för gruppen som du vill ta bort. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Du **måste** använda begärandehuvudet `x-sandbox-id` i stället för begärandehuvudet `x-sandbox-name` när du använder den här slutpunkten med AWS.

+++ En exempelbegäran om att ta bort en sats.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Egenskap | Beskrivning |
| -------- | ----------- |
| `datasetId` | ID:t för datauppsättningen för den grupp som du vill ta bort. |
| `batchId` | ID:t för gruppen som du vill ta bort. |

>[!ENDTABS]

**Svar**

>[!IMPORTANT]
>
>Följande svar skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Ett lyckat svar returnerar information om den nyligen skapade borttagningsbegäran, inklusive ett unikt, systemgenererat, skrivskyddat ID för begäran. Detta kan användas för att slå upp begäran och kontrollera dess status. `"status"` för begäran när den skapas är `"NEW"` tills bearbetningen börjar. Värdet `"batchId"` i svaret ska matcha värdet `"batchId"` som skickades i begäran.

+++ Ett svar på begäran om borttagning.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `id` | Det unika, systemgenererade skrivskyddade ID:t för borttagningsbegäran. |
| `datasetId` | ID för den angivna datauppsättningen. |
| `batchId` | Batchens ID, enligt POST-begäran. |

+++

>[!TAB Amazon Web Services (AWS)]

Ett lyckat svar returnerar information om den nyligen skapade systembegäran.

+++ Ett svar på begäran om borttagning.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `requestId` | ID:t för systemjobbet. |
| `requestType` | Systemjobbets typ. Möjliga värden är `BACKFILL_TTL`, `DELETE_EE_BATCH` och `TRUNCATE_DATASET`. |
| `status` | Systemjobbets status. Möjliga värden är `NEW`, `SUCCESS`, `ERROR`, `FAILED` och `IN-PROGRESS`. |
| `properties` | Ett objekt som innehåller batch- och/eller datauppsättnings-ID för systemjobbet. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>Följande funktion är **endast** tillgänglig när du använder Experience Platform på Microsoft Azure.

Om du försöker initiera en borttagningsbegäran för en postdatauppsättningsbatch kommer du att få ett 400-nivåfel, som följande:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Visa en specifik borttagningsbegäran {#view-a-specific-delete-request}

Om du vill visa en specifik borttagningsbegäran, inklusive information om dess status, kan du utföra en sökningsbegäran (GET) till `/system/jobs`-slutpunkten och inkludera ID:t för borttagningsbegäran i sökvägen.

**API-format**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | ID:t för den borttagningsbegäran som du vill visa. |

**Begäran**

>[!IMPORTANT]
>
>Följande begäran skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Ett exempel på en förfrågan om att visa ett profiljobb.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>Du **måste** använda begärandehuvudet `x-sandbox-id` i stället för begärandehuvudet `x-sandbox-name` när du använder den här slutpunkten med AWS.

+++ Ett exempel på en förfrågan om att visa ett profiljobb.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Svar**

>[!IMPORTANT]
>
>Följande svar skiljer sig mellan Azure- och AWS-instanserna.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

Svaret innehåller information om borttagningsbegäran, inklusive dess uppdaterade status. ID:t för borttagningsbegäran i svaret (värdet `"id"`) ska matcha det ID som skickades i begärandesökvägen.

+++ Ett godkänt svar för att visa en borttagningsbegäran.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Egenskaper | Beskrivning |
| ---------- | ----------- |
| `jobType` | Den typ av jobb som skapas returnerar alltid `"DELETE"`. |
| `status` | Status för borttagningsbegäran. Möjliga värden är `NEW`, `PROCESSING`, `COMPLETED` och `ERROR`. |
| `metrics` | En matris som innehåller antalet poster som har bearbetats (`"recordsProcessed"`) och tiden i sekunder som begäran har bearbetats, eller hur lång tid det tog att slutföra begäran (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

Ett lyckat svar returnerar information om den angivna systembegäran.

+++ Ett godkänt svar för att visa en borttagningsbegäran.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `requestId` | ID:t för systemjobbet. |
| `requestType` | Systemjobbets typ. Möjliga värden är `BACKFILL_TTL`, `DELETE_EE_BATCH` och `TRUNCATE_DATASET`. |
| `status` | Systemjobbets status. Möjliga värden är `NEW`, `SUCCESS`, `ERROR`, `FAILED` och `IN-PROGRESS`. |
| `properties` | Ett objekt som innehåller batch- och/eller datauppsättnings-ID för systemjobbet. |

+++

>[!ENDTABS]

När status för borttagningsbegäran är `"COMPLETED"` kan du bekräfta att data har tagits bort genom att försöka komma åt borttagna data med API:t för dataåtkomst. Instruktioner om hur du använder API:t för dataåtkomst för att komma åt datauppsättningar och grupper finns i [dokumentationen för dataåtkomst](../../data-access/home.md).

## Ta bort en borttagningsbegäran

>[!AVAILABILITY]
>
>Den här slutpunkten stöds **endast** i Azure-instansen av Adobe Experience Platform och **stöds inte** i AWS-instansen.

Med [!DNL Experience Platform] kan du ta bort en tidigare begäran, vilket kan vara användbart av flera anledningar, bland annat om borttagningsjobbet inte slutfördes eller fastnade i bearbetningsfasen. Om du vill ta bort en borttagningsbegäran kan du utföra en DELETE-begäran till `/system/jobs`-slutpunkten och inkludera ID:t för borttagningsbegäran som du vill ta bort till begärandesökvägen.

**API-format**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | ID för den borttagningsbegäran som du vill ta bort. |

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

En slutförd borttagningsbegäran returnerar HTTP-status 200 (OK) och en tom svarstext. Du kan bekräfta att begäran togs bort genom att utföra en GET-begäran för att visa borttagningsbegäran med dess ID. Detta bör returnera HTTP-status 404 (Hittades inte), vilket anger att borttagningsbegäran togs bort.

## Nästa steg

Nu när du vet vilka steg som ingår i att ta bort datauppsättningar och batchar från [!DNL Profile store] i [!DNL Experience Platform] kan du ta bort data som har lagts till felaktigt eller som din organisation inte längre behöver. Observera att det inte går att ångra en borttagningsbegäran. Du bör därför bara ta bort data som du är säker på att du inte behöver nu och inte behöver i framtiden.
