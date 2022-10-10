---
keywords: Experience Platform;hem;populära ämnen;flödestjänst;
title: (Beta) Skapa en flödeskörning för behovsstyrd inmatning med API:t för flödestjänsten
description: I den här självstudiekursen beskrivs stegen för att skapa ett flöde för on-demand-inmatning med API:t för Flow Service
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# (Beta) Skapa en flödeskörning för on-demand-förtäring med [!DNL Flow Service] API

>[!IMPORTANT]
>
>Intag på begäran finns för närvarande i betaversionen och din organisation har kanske inte tillgång till den än. Funktionerna som beskrivs i den här dokumentationen kan komma att ändras.

Flödeskörningar representerar en instans av flödeskörning. Om ett flöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

Intag på begäran ger dig möjlighet att skapa ett flöde som körs mot ett givet dataflöde. Detta gör att dina användare kan skapa en flödeskörning baserat på givna parametrar och skapa en insatscykel, utan tjänstens tokens. Stöd för on-demand-konsumtion finns endast för batchkällor.

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
          "startTime": "1663735590",
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
| `params.startTime` | Ett heltal som definierar körningens starttid. Värdet representeras i Unix Epooch-tid. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.deltaColumn` | Deltakolumnen krävs för att partitionera data och separera nyimporterade data från historiska data. **Anteckning**: The `deltaColumn` behövs bara när du skapar ditt första flöde. |
| `params.deltaColumn.name` | Namnet på deltakolumnen. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade flödeskörningen, inklusive dess unika körning `id`.

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för den nyligen skapade flödeskörningen. Se guiden [hämta flödesspecifikationer](../api/collect/database-nosql.md#specs) för mer information om tabellbaserade körningsspecifikationer. |
| `etag` | Resursversionen av flödeskörningen. |
<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

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
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| Parameter | Beskrivning |
| --- | --- |
| `flowId` | ID:t för det flöde som flödeskörningen ska skapas mot. |
| `params.startTime` | Ett heltal som definierar körningens starttid. Värdet representeras i Unix Epooch-tid. |
| `params.windowStartTime` | Ett heltal som definierar starttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |
| `params.windowEndTime` | Ett heltal som definierar sluttiden för det fönster där data ska hämtas. Värdet representeras i unix-tid. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade flödeskörningen, inklusive dess unika körning `id`.


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för den nyligen skapade flödeskörningen. Se guiden [hämta flödesspecifikationer](../api/collect/database-nosql.md#specs) för mer information om tabellbaserade körningsspecifikationer. |
| `etag` | Resursversionen av flödeskörningen. |

## Övervaka flödeskörningar

När flödeskörningen har skapats kan du övervaka de data som importeras genom den för att se information om flödeskörningar, slutförandestatus och fel. Om du vill övervaka ditt flöde med API kan du se självstudiekursen om [övervaka dataflöden i API ](./monitor.md). Om du vill övervaka ditt flöde med hjälp av plattformsgränssnittet läser du i handboken på [övervaka källfilsflöden med kontrollpanelen](../../../dataflows/ui/monitor-sources.md).
