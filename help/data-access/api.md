---
keywords: Experience Platform;hem;populära ämnen;dataåtkomst;python sdk;spark sdk;dataåtkomst api;export;Exportera
solution: Experience Platform
title: API-guide för dataåtkomst
description: API:t för dataåtkomst stöder Adobe Experience Platform genom att ge utvecklarna ett RESTful-gränssnitt som fokuserar på att upptäcka och tillgängliggöra inkapslade datauppsättningar i Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: d8694c094ae4a7284e4a3ed0ae5bc3dc198e501a
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 1%

---

# API-guide för dataåtkomst

API:t för dataåtkomst stöder Adobe Experience Platform genom att ge användarna ett RESTful-gränssnitt som fokuserar på att upptäcka och tillgängliggöra inkapslade datauppsättningar i [!DNL Experience Platform].

![Ett diagram över hur dataåtkomst gör det lättare att upptäcka och tillgängliggöra importerade datauppsättningar i Experience Platform.](images/Data_Access_Experience_Platform.png)

## API-specifikationsreferens

Referenshandboken för Swagger API finns [här](https://developer.adobe.com/experience-platform-apis/references/data-access/).

## Terminologi {#terminology}

Tabellen innehåller en beskrivning av några termer som används ofta i det här dokumentet.

| Term | Beskrivning |
| ----- | ------------ |
| Datauppsättning | En samling data som innehåller ett schema och fält. |
| Grupp | En uppsättning data som samlats in under en tidsperiod och som bearbetas tillsammans som en enda enhet. |

## Hämta en lista med filer i en grupp {#retrieve-list-of-files-in-a-batch}

Om du vill hämta en lista med filer som tillhör en viss grupp använder du batch-ID:t (batchID) med API:t för dataåtkomst.

**API-format**

```http
GET /batches/{BATCH_ID}/files
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | ID för den angivna batchen. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

The `"data"` arrayen innehåller en lista med alla filer i den angivna gruppen. Varje returnerad fil har ett eget unikt ID (`{FILE_ID}`) som finns i `"dataSetFileId"` fält. Du kan använda detta unika ID för att komma åt eller hämta filen.

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.dataSetFileId` | Fil-ID för varje fil i den angivna gruppen. |
| `data._links.self.href` | Den URL som ska användas för att komma åt filen. |

## Få tillgång till och ladda ned filer i en grupp

Om du vill komma åt specifik information om en fil använder du en filidentifierare (`{FILE_ID}`) med API:t för dataåtkomst, inklusive namn, storlek i byte och en länk som ska hämtas.

Svaret innehåller en datamatris. Beroende på om filen som ID:t pekar på är en enskild fil eller en katalog, kan den returnerade datarrayen innehålla en enda post eller en lista med filer som tillhör den katalogen. Varje filelement innehåller information om filen.

**API-format**

```http
GET /files/{FILE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | Lika med `"dataSetFileId"`, ID:t för filen som ska användas. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar på enstaka fil**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.name` | Filens namn (till exempel `profiles.csv`). |
| `data.length` | Filens storlek (i byte). |
| `data._links.self.href` | Den URL som filen ska hämtas från. |

**Katalogsvar**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

När en katalog returneras innehåller den en array med alla filer i katalogen.

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.name` | Filens namn (till exempel `profiles.csv`). |
| `data._links.self.href` | Den URL som filen ska hämtas från. |

## Åtkomst till innehållet i en fil {#access-file-contents}

Du kan också använda [!DNL Data Access] API för att komma åt innehållet i en fil. Du kan sedan hämta innehållet till en extern källa.

**API-format**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_NAME}` | Namnet på filen som du försöker komma åt. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | ID för filen i en datauppsättning. |
| `{FILE_NAME}` | Filens fullständiga namn (till exempel `profiles.csv`). |

**Svar**

`Contents of the file`

## Ytterligare kodexempel

Ytterligare exempel finns i [dataåtkomst, genomgång](tutorials/dataset-data.md).

## Prenumerera på dataöverföringshändelser {#subscribe-to-data-ingestion-events}

Du kan prenumerera på specifika värdefulla händelser via [Adobe Developer Console](https://developer.adobe.com/console/). Du kan t.ex. prenumerera på dataöverföringshändelser för att få meddelanden om eventuella förseningar och fel. Se självstudiekursen om [prenumerera på meddelanden om dataöverföring](../ingestion/quality/subscribe-events.md) för mer information.
