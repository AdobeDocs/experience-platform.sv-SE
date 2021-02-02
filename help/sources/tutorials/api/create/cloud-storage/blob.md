---
keywords: Experience Platform;hem;populära ämnen;Azure;azure blob;blob;blob
solution: Experience Platform
title: Skapa en Azure Blob-koppling med API:t för Flow Service
topic: overview
type: Tutorial
description: I den här självstudien används API:t för Flow Service för att vägleda dig genom stegen för att ansluta Experience Platform till en Azure Blob-lagring (nedan kallad Blob-lagring).
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Skapa en [!DNL Azure Blob]-koppling med hjälp av API:t [!DNL Flow Service]

I den här självstudien används [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) för att vägleda dig genom stegen för att ansluta [!DNL Azure Blob] (nedan kallat &quot;Blob&quot;) till Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Blob]-källkoppling med hjälp av API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till ditt [!DNL Blob]-lagringsutrymme måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | En sträng som innehåller den auktoriseringsinformation som krävs för att autentisera [!DNL Blob] till Experience Platform. Anslutningssträngsmönstret [!DNL Blob] är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i det här [!DNL Blob]-dokumentet om [konfigurering av anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt [!DNL Blob]-konto. SAS-URI-mönstret [!DNL Blob] är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i det här [!DNL Blob]-dokumentet på [URI:er för delad åtkomst](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för [!DNL Blob] är: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [hur du läser exempel-API-anrop](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till plattforms-API:er måste du först slutföra [självstudiekursen](https://www.adobe.com/go/platform-api-authentication-en) för autentisering. När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör [!DNL Flow Service], isoleras till specifika virtuella sandlådor. Alla begäranden till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

* `x-sandbox-name: {SANDBOX_NAME}`

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en medietypsrubrik:

* `Content-Type: application/json`

## Skapa en anslutning

En anslutning anger en källa och innehåller dina autentiseringsuppgifter för den källan. Endast en anslutning krävs per [!DNL Blob]-konto eftersom den kan användas för att skapa flera dataflöden för att hämta olika data.

### Skapa en [!DNL Blob]-anslutning med anslutningssträngsbaserad autentisering

Om du vill skapa en [!DNL Blob]-anslutning med hjälp av anslutningssträngsbaserad autentisering kan du göra en POST-förfrågan till API:t [!DNL Flow Service] samtidigt som du anger [!DNL Blob] `connectionString`.

**API-format**

```http
POST /connections
```

**Begäran**

För att kunna skapa en [!DNL Blob]-anslutning måste dess unika anslutningsspecifikations-ID anges som en del av POSTEN. Anslutningsspecifikationens ID för [!DNL Blob] är `4c10e202-c428-4796-9208-5f1f5732b1cf`.

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

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska ditt lagringsutrymme i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Skapa en [!DNL Blob]-anslutning med signatur-URI för delad åtkomst

En SAS-URI (Shared Access Signature) möjliggör säker delegerad auktorisering till ditt [!DNL Blob]-konto. Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Om du vill skapa en [!DNL Blob]-anslutning med hjälp av en URI för signatur för delad åtkomst gör du en POST-förfrågan till API:t [!DNL Flow Service] samtidigt som du anger värden för [!DNL Blob] `sasUri`.

**API-format**

```http
POST /connections
```

**Begäran**

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

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska ditt lagringsutrymme i nästa självstudiekurs.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en [!DNL Blob]-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för flödestjänst](../../explore/cloud-storage.md) eller [import av Parquet-data med API:t för flödestjänst](../../cloud-storage-parquet.md).