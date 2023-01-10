---
keywords: Experience Platform;hem;populära ämnen;Azure Data Lake Storage Gen2;Azure Data Lake Storage Storage;Azure
solution: Experience Platform
title: Skapa en Azure Data Lake Storage Gen2 Base-anslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter Adobe Experience Platform till Azure Data Lake Storage Gen2 med API:t för Flow Service.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Skapa en [!DNL Azure Data Lake Storage Gen2] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Azure Data Lake Storage Gen2] (nedan kallat ADLS Gen2) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna skapa en ADLS Gen2-källanslutning med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] Om du vill ansluta till ADLS Gen2 måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | Slutpunkten för ADLS Gen2. Slutpunktsmönstret är: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | Programmets klient-ID. |
| `servicePrincipalKey` | Programmets nyckel. |
| `tenant` | Klientinformationen som innehåller ditt program. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för ADLS Gen2 är: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Mer information om dessa värden finns i [det här ADLS Gen2-dokumentet](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkten när du anger dina ADLS Gen2-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för ADLS Gen2:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.url` | URL-slutpunkten för ditt ADLS Gen2-konto. |
| `auth.params.servicePrincipalId` | Tjänstens huvud-ID för ditt ADLS Gen2-konto. |
| `auth.params.servicePrincipalKey` | Tjänstens huvudnyckel för ADLS Gen2-kontot. |
| `auth.params.tenant` | Klientinformation för ditt ADLS Gen2-konto. |
| `connectionSpec.id` | ADLS Gen2-anslutningsspecifikations-ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Nästa steg

I den här självstudiekursen har du skapat en ADLS Gen2-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
