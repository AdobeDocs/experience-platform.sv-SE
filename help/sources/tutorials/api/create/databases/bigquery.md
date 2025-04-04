---
title: Anslut Google BigQuery till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Google BigQuery med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Anslut [!DNL Google BigQuery] till Experience Platform med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Google BigQuery] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill lära dig hur du ansluter din [!DNL Google BigQuery]-databas till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Google BigQuery] autentiseringsguiden](../../../../connectors/databases/bigquery.md#prerequisites) om du vill ha mer information om hur du hämtar dina [!DNL Google BigQuery]-autentiseringsuppgifter.

## Anslut [!DNL Google BigQuery] till Experience Platform på Azure {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Google BigQuery]-källa till Experience Platform på Azure.

### Skapa en basanslutning för [!DNL Google BigQuery] på Experience Platform på Azure {#azure-base}

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Google BigQuery]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Använd grundläggande autentisering]

+++Begäran

Följande begäran skapar en basanslutning för [!DNL Google BigQuery] med grundläggande autentisering.

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

+++

+++svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Använd tjänstautentisering]


+++Begäran

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

+++

+++svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Anslut [!DNL Google BigQuery] till Experience Platform på Amazon Web Services (AWS) {#aws}

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Google BigQuery]-databas till Experience Platform på AWS.

### Skapa en basanslutning för [!DNL Google BigQuery] på Experience Platform på AWS

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för att ansluta [!DNL Google BigQuery] till Experience Platform på AWS.

+++Markera för att visa exempel

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.projectId` | Projekt-ID för standardprojektet [!DNL Google BigQuery] som ska frågas. mot. |
| `auth.params.keyFileContent` | Nyckelfilen som används för att autentisera tjänstkontot. Du måste koda nyckelfilens innehåll i [!DNL Base64]. |
| `auth.params.datasetId` | Det datauppsättnings-ID som motsvarar din [!DNL Google BigQuery]-källa. Detta ID representerar var datatabellerna finns. |

+++

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska ditt lagringsutrymme i nästa självstudiekurs.

+++Markera för att visa exempel

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Google BigQuery]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
