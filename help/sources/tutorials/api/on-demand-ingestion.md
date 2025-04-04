---
keywords: Experience Platform;home;populära topics;flow service;
title: Skapa en flödeskörning för behovsstyrd matning med API:t för flödestjänsten
description: Lär dig hur du skapar en flödeskörning för on-demand-inmatning med API:t för Flow Service
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# Skapa en flödeskörning för on-demand-inmatning med API:t [!DNL Flow Service]

Flödeskörningar representerar en instans av flödeskörning. Om ett flöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

Intag på begäran ger dig möjlighet att skapa ett flöde som körs mot ett givet dataflöde. Detta gör att dina användare kan skapa en flödeskörning baserat på givna parametrar och skapa en insatscykel, utan tjänstens tokens. Stöd för on-demand-konsumtion finns endast för batchkällor.

I den här självstudiekursen beskrivs hur du använder on-demand-inmatning och skapar en flödeskörning med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

>[!NOTE]
>
>För att kunna skapa en flödeskörning måste du först ha flödes-ID:t för ett dataflöde som är schemalagt för engångsinmatning.

Den här självstudiekursen kräver att du har en fungerande förståelse för följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../landing/api-guide.md).

## Skapa en flödeskörning för en tabellbaserad källa

Om du vill skapa ett flöde för en tabellbaserad källa skapar du en POST-begäran till [!DNL Flow Service]-API:t och anger ID:t för det flöde som du vill skapa körningen mot, samt värden för starttid, sluttid och delta-kolumn.

>[!TIP]
>
>Tabellbaserade källor omfattar följande källkategorier: annonsering, analys, samtycke och preferenser, CRM, kundframgångar, databas, automatiserad marknadsföring, betalningar och protokoll.

**API-format**

```http
POST /runs/
```

**Begäran**

Följande begäran skapar en flödeskörning för flödes-ID `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>Du behöver bara ange `deltaColumn` när du skapar din första flödeskörning. Efter det kommer `deltaColumn` att korrigeras som en del av `copy`-omformningen i flödet och behandlas som sanningens källa. Alla försök att ändra värdet `deltaColumn` via flödeskörningsparametrarna resulterar i ett fel.

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
| `params.startTime` | Den schemalagda tiden då flödeskörningen på begäran börjar. Detta värde representeras i unix-tid. |
| `params.windowStartTime` | Det tidigaste datum och den tidigaste tid som data hämtas från. Detta värde representeras i unix-tid. |
| `params.windowEndTime` | Datum och tid då data hämtas fram till. Detta värde representeras i unix-tid. |
| `params.deltaColumn` | Deltakolumnen krävs för att partitionera data och separera nyimporterade data från historiska data. **Obs!** `deltaColumn` behövs bara när du skapar ditt första flöde. |
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
| `id` | ID för den nyligen skapade flödeskörningen. Mer information om tabellbaserade körningsspecifikationer finns i guiden [Hämta flödesspecifikationer](../api/collect/database-nosql.md#specs). |
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

Om du vill skapa ett flöde för en filbaserad källa gör du en POST-begäran till [!DNL Flow Service]-API:t och anger ID:t för det flöde som du vill skapa körningen mot och värden för starttid och sluttid.

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
| `params.startTime` | Den schemalagda tiden då flödeskörningen på begäran börjar. Detta värde representeras i unix-tid. |
| `params.windowStartTime` | Det tidigaste datum och den tidigaste tid som data hämtas från. Detta värde representeras i unix-tid. |
| `params.windowEndTime` | Datum och tid då data hämtas fram till. Detta värde representeras i unix-tid. |

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
| `id` | ID för den nyligen skapade flödeskörningen. Mer information om tabellbaserade körningsspecifikationer finns i guiden [Hämta flödesspecifikationer](../api/collect/database-nosql.md#specs). |
| `etag` | Resursversionen av flödeskörningen. |

## Övervaka flödeskörningar

När flödeskörningen har skapats kan du övervaka de data som importeras genom den för att se information om flödeskörningar, slutförandestatus och fel. Om du vill övervaka ditt flöde med API kan du läsa självstudiekursen om [övervakning av dataflöden i API:t](./monitor.md). Om du vill övervaka ditt flöde med hjälp av Experience Platform UI läser du i guiden [Övervaka källfilsflöden med kontrollpanelen](../../../dataflows/ui/monitor-sources.md).
