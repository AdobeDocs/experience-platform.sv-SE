---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utvecklarhandbok för dataåtkomst
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---


# Utvecklarhandbok för dataåtkomst

API:t för dataåtkomst stöder Adobe Experience Platform genom att ge användarna ett RESTful-gränssnitt som fokuserar på identifierbarhet och tillgänglighet för kapslade datauppsättningar i [!DNL Experience Platform].

![Dataåtkomst i Experience Platform](images/Data_Access_Experience_Platform.png)

## API-specifikationsreferens

Referensdokumentationen för Swagger API finns [här](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologi

En beskrivning av några vanliga termer i det här dokumentet.

| Term | Beskrivning |
| ----- | ------------ |
| Datauppsättning | En samling data som innehåller schema och fält. |
| Grupp | En uppsättning data som samlats in under en tidsperiod och som bearbetas tillsammans som en enda enhet. |

## Hämta en lista med filer i en grupp

Genom att använda en batch-ID (batch-ID) kan API:t för dataåtkomst hämta en lista över filer som tillhör den aktuella gruppen.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Arrayen innehåller en lista med alla filer i den angivna gruppen. `"data"` Varje returnerad fil har ett eget unikt ID (`{FILE_ID}`) som finns i `"dataSetFileId"` fältet. Detta unika ID kan sedan användas för att komma åt eller hämta filen.

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data.dataSetFileId` | Fil-ID för varje fil i den angivna gruppen. |
| `data._links.self.href` | Den URL som ska användas för att komma åt filen. |

## Få tillgång till och ladda ned filer i en grupp

Genom att använda en filidentifierare (`{FILE_ID}`) kan API:t för dataåtkomst användas för att komma åt specifik information om en fil, inklusive filens namn, storlek i byte och en länk som ska hämtas.

Svaret innehåller en datamatris. Beroende på om filen som ID:t pekar på är en enskild fil eller en katalog, kan den returnerade datarrayen innehålla en enda post eller en lista med filer som tillhör den katalogen. Varje filelement innehåller information om filen.

**API-format**

```http
GET /files/{FILE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | Samma som `"dataSetFileId"`ID:t för filen som ska öppnas. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | Filens namn (t.ex. profiles.csv). |
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
| `data.name` | Filens namn (t.ex. profiles.csv). |
| `data._links.self.href` | Den URL som filen ska hämtas från. |

## Åtkomst till innehållet i en fil

API:t kan också användas för att komma åt innehållet i en fil [!DNL Data Access] . Den kan sedan användas för att hämta innehållet till en extern källa.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | ID för filen i en datauppsättning. |
| `{FILE_NAME}` | Filens fullständiga namn (t.ex. profiles.csv). |

**Svar**

```
Contents of the file
```

## Ytterligare kodexempel

Ytterligare exempel finns i [dataåtkomstsjälvstudiekursen](tutorials/dataset-data.md).

## Prenumerera på dataöverföringshändelser

[!DNL Platform] gör specifika värdefulla händelser tillgängliga för prenumeration via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Du kan t.ex. prenumerera på dataöverföringshändelser för att få meddelanden om eventuella förseningar och fel. Mer information finns i självstudiekursen om hur du [prenumererar på meddelanden](../ingestion/quality/subscribe-events.md) om dataöverföring.