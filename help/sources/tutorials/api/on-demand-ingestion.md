---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;
title: (Beta) Skapa en flödeskörning för behovsstyrd inmatning med API:t för flödestjänsten
description: I den här självstudiekursen beskrivs stegen för att skapa ett flöde för on-demand-inmatning med API:t för Flow Service
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 659f99a47b533bba2a6084bc8e235df2a29a6386
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# (Beta) Skapa en flödeskörning för on-demand-förtäring med [!DNL Flow Service] API

>[!IMPORTANT]
>
>Intag på begäran finns för närvarande i betaversionen och din organisation har kanske inte tillgång till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Flödeskörningar representerar en instans av flödeskörning. Om ett flöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

Intag på begäran ger dig möjlighet att skapa ett flöde som körs mot ett givet dataflöde. Detta gör att dina användare kan skapa en flödeskörning baserat på givna parametrar och skapa en insatscykel, utan tjänstens tokens.

I den här självstudiekursen beskrivs hur du använder on-demand-inmatning och skapar ett flöde med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

>[!NOTE]
>
>För att kunna skapa en flödeskörning måste du först ha flödes-ID:t för ett dataflöde som är schemalagt för engångsintag.

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../landing/api-guide.md).

## Skapa en flödeskörning för en tabellbaserad källa

Om du vill skapa ett flöde för en tabellbaserad källa skickar du en POST till [!DNL Flow Service] API när du anger ID:t för det flöde som du vill köra mot samt värden för starttid, sluttid och deltakolumn.

>[!TIP]
>
>Tabellbaserade källor innehåller följande källkategorier: annonsering, analys, samtycke och preferenser, CRM, kundframgångar, databas, automatiserad marknadsföring, betalningar och protokoll.

**API-format**

```http
POST /runs/
```

**Begäran**

Följande begäran skapar en flödeskörning för flödes-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Du behöver bara ange `deltaColumn` när du skapar din första flödeskörning. Efter det `deltaColumn` kommer att korrigeras som en del av `copy` förändringen i flödet och kommer att behandlas som källan till sanning. Eventuella försök att ändra `deltaColumn` värdet via flödeskörningsparametrarna resulterar i ett fel.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `flowId` | ID:t för det flöde som flödeskörningen ska skapas mot. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.deltaColumn` | Deltakolumnen krävs för att partitionera data och separera nyimporterade data från historiska data. |
| `params.deltaColumn.name` | Namnet på deltakolumnen. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade flödeskörningen, inklusive dess unika körning `id`.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för den nyligen skapade flödeskörningen. Se guiden [hämta flödesspecifikationer](../api/collect/database-nosql.md#specs) för mer information om tabellbaserade körningsspecifikationer. |
| `createdAt` | Unix-tidsstämpeln som anger när flödeskörningen skapades. |
| `updatedAt` | Unix-tidsstämpeln som anger när flödeskörningen senast uppdaterades. |
| `createdBy` | Organisations-ID för användaren som skapade flödeskörningen. |
| `updatedBy` | Organisations-ID för den användare som senast uppdaterade flödeskörningen. |
| `createdClient` | Programklienten som skapade flödeskörningen. |
| `updatedClient` | Programklienten som senast uppdaterade flödeskörningen. |
| `sandboxId` | ID:t för sandlådan som innehåller flödeskörningen. |
| `sandboxName` | Namnet på sandlådan som innehåller flödeskörningen. |
| `imsOrgId` | Organisations-ID. |
| `flowId` | ID för det flöde som flödeskörningen skapas mot. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.deltaColumn` | Deltakolumnen krävs för att partitionera data och separera nyimporterade data från historiska data. **Anteckning**: The `deltaColumn` behövs bara när du skapar ditt första flöde. |
| `params.deltaColumn.name` | Namnet på deltakolumnen. |
| `etag` | Resursversionen av flödeskörningen. |
| `metrics` | Den här egenskapen visar en statussammanfattning för flödeskörningen. |

## Skapa en flödeskörning för en filbaserad källa

Om du vill skapa ett flöde för en filbaserad källa skickar du en POST till [!DNL Flow Service] API när du anger ID:t för det flöde du vill skapa körningen mot och värden för start- och sluttid.

>[!TIP]
>
>Filbaserade källor innehåller alla molnlagringskällor.

**API-format**

```http
POST /runs/
```

**Begäran**

Följande begäran skapar en flödeskörning för flödes-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `flowId` | ID:t för det flöde som flödeskörningen ska skapas mot. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade flödeskörningen, inklusive dess unika körning `id`.


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för den nyligen skapade flödeskörningen. Se guiden [hämta flödesspecifikationer](../api/collect/cloud-storage.md#specs) för mer information om filbaserade körningsspecifikationer. |
| `createdAt` | Unix-tidsstämpeln som anger när flödeskörningen skapades. |
| `updatedAt` | Unix-tidsstämpeln som anger när flödeskörningen senast uppdaterades. |
| `createdBy` | Organisations-ID för användaren som skapade flödeskörningen. |
| `updatedBy` | Organisations-ID för den användare som senast uppdaterade flödeskörningen. |
| `createdClient` | Programklienten som skapade flödeskörningen. |
| `updatedClient` | Programklienten som senast uppdaterade flödeskörningen. |
| `sandboxId` | ID:t för sandlådan som innehåller flödeskörningen. |
| `sandboxName` | Namnet på sandlådan som innehåller flödeskörningen. |
| `imsOrgId` | Organisations-ID. |
| `flowId` | ID för det flöde som flödeskörningen skapas mot. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `etag` | Resursversionen av flödeskörningen. |
| `metrics` | Den här egenskapen visar en statussammanfattning för flödeskörningen. |


## Övervaka flödeskörningar

När flödeskörningen har skapats kan du övervaka de data som importeras genom den för att se information om flödeskörningar, slutförandestatus och fel. Om du vill övervaka ditt flöde med API kan du se självstudiekursen om [övervaka dataflöden i API ](./monitor.md). Om du vill övervaka ditt flöde med hjälp av plattformsgränssnittet läser du i handboken på [övervaka källfilsflöden med kontrollpanelen](../../../dataflows/ui/monitor-sources.md).
