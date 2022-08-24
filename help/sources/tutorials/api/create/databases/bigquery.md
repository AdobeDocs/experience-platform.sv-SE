---
keywords: Experience Platform;hem;populära ämnen;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Skapa en Google BigQuery Base-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Google BigQuery med API:t för Flow Service.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 015a4fa06fc2157bb8374228380bb31826add37e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Skapa en [!DNL Google BigQuery] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Google BigQuery] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Google BigQuery] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att ansluta [!DNL Google BigQuery] På Platform måste du ange följande OAuth 2.0-autentiseringsvärden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `project` | Standardprojektets ID [!DNL Google BigQuery] projekt att fråga efter. |
| `clientID` | ID-värdet som används för att generera uppdateringstoken. |
| `clientSecret` | Det hemliga värde som används för att generera uppdateringstoken. |
| `refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] används för att auktorisera åtkomst till [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | Det färdiga  [!DNL Google BigQuery] ID för datauppsättning som krävs för att aktivera stöd för stora resultatuppsättningar. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Google BigQuery] är: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Mer information om dessa värden finns i [[!DNL Google BigQuery] dokument](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Google BigQuery] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Google BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `auth.params.project` | Standardprojektets ID [!DNL Google BigQuery] projekt att fråga efter. mot. |
| `auth.params.clientId` | ID-värdet som används för att generera uppdateringstoken. |
| `auth.params.clientSecret` | Klientvärdet som används för att generera uppdateringstoken. |
| `auth.params.refreshToken` | Uppdateringstoken som hämtats från [!DNL Google] används för att auktorisera åtkomst till [!DNL Google BigQuery]. |
| `connectionSpec.id` | The [!DNL Google BigQuery] anslutningsspecifikation-ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Svar**

Ett godkänt svar returnerar information om den nya anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Google BigQuery] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
