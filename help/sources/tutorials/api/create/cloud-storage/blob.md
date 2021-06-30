---
keywords: Experience Platform;hem;populära ämnen;Azure;azure blob;blob;blob
solution: Experience Platform
title: Skapa en Azure Blob Base-anslutning med API:t för Flow Service
topic-legacy: overview
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Azure Blob med API:t för Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Skapa en [!DNL Azure Blob]-basanslutning med hjälp av API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Azure Blob] (kallas nedan &quot;[!DNL Blob]&quot;) med hjälp av [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Blob]-källanslutning med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Blob]-lagringsutrymme måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En sträng som innehåller den auktoriseringsinformation som krävs för att autentisera [!DNL Blob] till Experience Platform. Anslutningssträngsmönstret [!DNL Blob] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i det här [!DNL Blob]-dokumentet om [konfigurering av anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt [!DNL Blob]-konto. SAS-URI-mönstret [!DNL Blob] är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i det här [!DNL Blob]-dokumentet på [URI:er för delad åtkomst](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Blob] är: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Använda plattforms-API:er

Information om hur du kan anropa API:er för plattformar finns i guiden [komma igång med API:er för plattformar](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett grundläggande anslutnings-ID skickar du en POST till `/connections`-slutpunkten och anger dina autentiseringsuppgifter för [!DNL Blob] som en del av parametrarna för begäran.

### Skapa en [!DNL Blob]-basanslutning med anslutningssträngsbaserad autentisering

Om du vill skapa en [!DNL Blob]-basanslutning med hjälp av anslutningssträngsbaserad autentisering kan du göra en POST-förfrågan till API:t [!DNL Flow Service] samtidigt som du anger [!DNL Blob] `connectionString`.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Blob] med anslutningssträngsbaserad autentisering:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som krävs för att komma åt data i blobblagringen. Blobanslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Anslutningsspecifikation-ID för Blob-lagring är: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Skapa en [!DNL Blob]-basanslutning med hjälp av URI för signatur med delad åtkomst

En SAS-URI (Shared Access Signature) möjliggör säker delegerad auktorisering till ditt [!DNL Blob]-konto. Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Om du vill skapa en [!DNL Blob]-blobbanslutning med en URI för signatur för delad åtkomst, gör du en POST-förfrågan till API:t [!DNL Flow Service] samtidigt som du anger värden för [!DNL Blob] `sasUri`.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Blob] med signatur-URI för delad åtkomst:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.connectionString` | Den SAS-URI som krävs för att komma åt data i ditt [!DNL Blob]-lagringsutrymme. SAS-URI-mönstret [!DNL Blob] är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | Specifikation-ID för lagringsanslutning för [!DNL Blob] är: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Blob]-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för flödestjänst](../../explore/cloud-storage.md) eller [import av Parquet-data med API:t för flödestjänst](../../cloud-storage-parquet.md).
