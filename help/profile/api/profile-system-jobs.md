---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: API-slutpunkt för profilsystemjobb
topic-legacy: guide
type: Documentation
description: Med Adobe Experience Platform kan du ta bort en datauppsättning eller en batch från profilbutiken för att ta bort kundprofildata i realtid som inte längre behövs eller som har lagts till av misstag. Detta kräver att du använder profil-API:t för att skapa ett profilsystemjobb eller för att ta bort en begäran.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 1%

---

# Slutpunkt för profilsystemjobb (Delete-begäranden)

Med Adobe Experience Platform kan ni importera data från flera olika källor och skapa robusta profiler för enskilda kunder. Data som hämtas till [!DNL Platform] lagras i [!DNL Data Lake], och om datauppsättningarna har aktiverats för Profil lagras även dessa data i [!DNL Real-time Customer Profile]-datalagret. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en batch från profilarkivet för att ta bort data som inte längre behövs eller som har lagts till av misstag. Detta kräver att du använder API:t [!DNL Real-time Customer Profile] för att skapa ett [!DNL Profile]-systemjobb, eller `delete request`, som också kan ändras, övervakas eller tas bort vid behov.

>[!NOTE]
>
>Om du försöker ta bort datauppsättningar eller grupper från [!DNL Data Lake] kan du få mer information genom att gå till [Katalogtjänstöversikt](../../catalog/home.md).

## Komma igång

API-slutpunkten som används i den här guiden är en del av [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Innan du fortsätter bör du läsa [kom igång-guiden](getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempel-API-anropen i det här dokumentet och viktig information om vilka huvuden som krävs för att anropa ett Experience Platform-API.

## Visa borttagningsbegäranden

En borttagningsbegäran är en långvarig, asynkron process, vilket innebär att din organisation kan köra flera borttagningsbegäranden samtidigt. Om du vill visa alla borttagningsbegäranden som din organisation för närvarande kör kan du utföra en GET-begäran till `/system/jobs`-slutpunkten.

Du kan också använda valfria frågeparametrar för att filtrera listan med borttagningsbegäranden som returneras i svaret. Om du vill använda flera parametrar avgränsar du varje parameter med ett et-tecken (`&`).

**API-format**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `start` | Förskjut den returnerade resultatsidan enligt skapandetiden för begäran. Exempel: `start=4` |
| `limit` | Begränsa antalet returnerade resultat. Exempel: `limit=10` |
| `page` | Returnera en specifik resultatsida enligt skapandetiden för begäran. Exempel: `page=2` |
| `sort` | Sortera resultaten efter ett specifikt fält i stigande (`asc`) eller fallande (`desc`) ordning. Sorteringsparametern fungerar inte när flera resultatsidor returneras. Exempel: `sort=batchId:asc` |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller en &quot;children&quot;-array med ett objekt för varje borttagningsbegäran som innehåller information om den begäran.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
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
|---|---|
| `_page.count` | Totalt antal begäranden. Svaret har trunkerats för utrymme. |
| `_page.next` | Om det finns ytterligare en resultatsida kan du visa nästa resultatsida genom att ersätta ID-värdet i en [sökbegäran](#view-a-specific-delete-request) med `"next"`-värdet. |
| `jobType` | Den typ av jobb som skapas. I det här fallet returneras alltid `"DELETE"`. |
| `status` | Status för borttagningsbegäran. Möjliga värden är `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Ett objekt som innehåller antalet poster som har bearbetats (`"recordsProcessed"`) och tiden i sekunder som begäran har bearbetats, eller hur lång tid det tog att slutföra begäran (`"timeTakenInSec"`). |

## Skapa en borttagningsbegäran {#create-a-delete-request}

Initieringen av en ny borttagningsbegäran görs via en begäran om POST till `/systems/jobs`-slutpunkten, där ID:t för den datauppsättning eller batch som ska tas bort anges i förfrågningens innehåll.

### Ta bort en datauppsättning

Om du vill ta bort en datauppsättning från profilarkivet måste datauppsättnings-ID:t inkluderas i POSTENS innehåll. Den här åtgärden tar bort ALLA data för en viss datauppsättning. [!DNL Experience Platform] Med kan du ta bort datauppsättningar baserat på både schema för post- och tidsserier.

**API-format**

```http
POST /system/jobs
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `dataSetId` | **(Obligatoriskt)** ID:t för den datauppsättning som du vill ta bort. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade borttagningsbegäran, inklusive ett unikt, systemgenererat, skrivskyddat ID för begäran. Detta kan användas för att slå upp begäran och kontrollera dess status. `status` för begäran när den skapas är `"NEW"` tills den börjar bearbetas. `dataSetId` i svaret ska matcha `dataSetId` som skickats i begäran.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Det unika, systemgenererade skrivskyddade ID:t för borttagningsbegäran. |
| `dataSetId` | Datauppsättningens ID, enligt POSTENS begäran. |

### Ta bort en grupp

Om du vill ta bort en batch måste batch-ID:t inkluderas i POSTENS innehåll. Observera att du inte kan ta bort grupper för datauppsättningar baserat på postscheman. Endast grupper för datauppsättningar som baseras på tidsseriescheman kan tas bort.

>[!NOTE]
>
> Orsaken till att du inte kan ta bort batchar för datauppsättningar baserade på postscheman är att datauppsättningsbatchar skriver över tidigare poster och därför inte kan ångras eller tas bort. Det enda sättet att ta bort effekten av felaktiga batchar för datauppsättningar som baseras på postscheman är att importera om gruppen med rätt data för att skriva över felaktiga poster.

Mer information om post- och tidsseriebeteende finns i [avsnittet om XDM-databeteenden](../../xdm/home.md#data-behaviors) i översikten [!DNL XDM System].

**API-format**

```http
POST /system/jobs
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Egenskap | Beskrivning |
|---|---|
| `batchId` | **(Obligatoriskt)** ID:t för gruppen som du vill ta bort. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade borttagningsbegäran, inklusive ett unikt, systemgenererat, skrivskyddat ID för begäran. Detta kan användas för att slå upp begäran och kontrollera dess status. `"status"` för begäran när den skapas är `"NEW"` tills den börjar bearbetas. Värdet `"batchId"` i svaret ska matcha det `"batchId"`-värde som skickades i begäran.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Egenskap | Beskrivning |
|---|---|
| `id` | Det unika, systemgenererade skrivskyddade ID:t för borttagningsbegäran. |
| `batchId` | Batchens ID, som anges i begäran om POST. |

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
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obligatoriskt)** ID:t för borttagningsbegäran som du vill visa. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Svaret innehåller information om borttagningsbegäran, inklusive dess uppdaterade status. ID:t för borttagningsbegäran i svaret (värdet `"id"`) ska matcha det ID som skickades i begärandesökvägen.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Egenskaper | Beskrivning |
|---|---|
| `jobType` | Den typ av jobb som skapas returnerar alltid `"DELETE"`. |
| `status` | Status för borttagningsbegäran. Möjliga värden: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | En array som innehåller antalet poster som har bearbetats (`"recordsProcessed"`) och tiden i sekunder som begäran har bearbetats, eller hur lång tid det tog att slutföra begäran (`"timeTakenInSec"`). |

När status för borttagningsbegäran är `"COMPLETED"` kan du bekräfta att data har tagits bort genom att försöka komma åt borttagna data med hjälp av API:t för dataåtkomst. Instruktioner om hur du använder API:t för dataåtkomst för att komma åt datauppsättningar och grupper finns i [dokumentationen för dataåtkomst](../../data-access/home.md).

## Ta bort en borttagningsbegäran

[!DNL Experience Platform] I kan du ta bort en tidigare begäran, vilket kan vara användbart av flera anledningar, bland annat om borttagningsjobbet inte slutfördes eller fastnade i bearbetningsfasen. Om du vill ta bort en borttagningsbegäran kan du utföra en DELETE-begäran till `/system/jobs`-slutpunkten och inkludera ID:t för den borttagningsbegäran som du vill ta bort till sökvägen för begäran.

**API-format**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parameter | Beskrivning |
|---|---|
| {DELETE_REQUEST_ID} | ID:t för den borttagningsbegäran som du vill ta bort. |

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

En slutförd borttagningsbegäran returnerar HTTP-status 200 (OK) och en tom svarstext. Du kan bekräfta att begäran har tagits bort genom att utföra en GET-begäran för att visa borttagningsbegäran med dess ID. Detta bör returnera HTTP-status 404 (Hittades inte), vilket anger att borttagningsbegäran togs bort.

## Nästa steg

Nu när du vet vilka steg det handlar om att ta bort datauppsättningar och grupper från [!DNL Profile Store] i [!DNL Experience Platform] kan du ta bort data som har lagts till felaktigt eller som din organisation inte längre behöver. Observera att det inte går att ångra en borttagningsbegäran. Du bör därför bara ta bort data som du är säker på att du inte behöver nu och inte behöver i framtiden.
