---
title: Skapa en Google BigQuery Base-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Google BigQuery med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Skapa en [!DNL Google BigQuery]-basanslutning med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Google BigQuery] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

Läs den här vägledningen när du vill lära dig hur du skapar en basanslutning för [!DNL Google BigQuery] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Google BigQuery] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Google BigQuery] autentiseringsguiden](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) om du vill ha mer information om hur du samlar in dina nödvändiga inloggningsuppgifter.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till slutpunkten `/connections` och anger dina autentiseringsuppgifter för [!DNL Google BigQuery] som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Använd grundläggande autentisering]

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Google BigQuery] med grundläggande autentisering:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
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
| `auth.params.project` | Projekt-ID för standardprojektet [!DNL Google BigQuery] som ska frågas. mot. |
| `auth.params.clientId` | ID-värdet som används för att generera uppdateringstoken. |
| `auth.params.clientSecret` | Klientvärdet som används för att generera uppdateringstoken. |
| `auth.params.refreshToken` | Uppdateringstoken från [!DNL Google] som används för att auktorisera åtkomst till [!DNL Google BigQuery]. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!TAB Använd tjänstautentisering]


**Begäran**

Följande begäran skapar en basanslutning för [!DNL Google BigQuery] med tjänstautentisering:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery base connection with service account",
        "description": "Google BigQuery connection with service account",
        "auth": {
            "specName": "Service Authentication",
            "params": {
                    "projectId": "{PROJECT_ID}",
                    "keyFileContent": "{KEY_FILE_CONTENT},
                    "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
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
| `auth.params.projectId` | Projekt-ID för standardprojektet [!DNL Google BigQuery] som ska frågas. mot. |
| `auth.params.keyFileContent` | Nyckelfilen som används för att autentisera tjänstkontot. Du måste koda nyckelfilens innehåll i [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Valfritt) Det förskapade [!DNL Google BigQuery]-datauppsättnings-ID som krävs för att aktivera stöd för stora resultatuppsättningar. |

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!ENDTABS]


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Google BigQuery]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/database-nosql.md)
