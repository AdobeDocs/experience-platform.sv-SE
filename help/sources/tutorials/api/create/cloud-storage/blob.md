---
title: Skapa en Azure Blob Base-anslutning med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Azure Blob med API:t för Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# Skapa en [!DNL Azure Blob] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen beskrivs hur du skapar en basanslutning för [!DNL Azure Blob] (nedan kallad[!DNL Blob]&quot;) med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna skapa en [!DNL Blob] källanslutning med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] för att få kontakt med [!DNL Blob] måste du ange värden för följande anslutningsegenskap:

>[!BEGINTABS]

>[!TAB Autentisering av anslutningssträng]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `connectionString` | En sträng som innehåller den auktoriseringsinformation som krävs för autentisering [!DNL Blob] till Experience Platform. The [!DNL Blob] anslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Mer information om anslutningssträngar finns i [!DNL Blob] dokument på [konfigurera anslutningssträngar](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Blob] är: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB SAS-URI-autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som alternativ autentiseringstyp för att ansluta [!DNL Blob] konto. The [!DNL Blob] SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Mer information finns i [!DNL Blob] dokument på [URI:er för delad åtkomstsignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Namnet på den behållare som du vill tilldela åtkomst till. När du skapar ett nytt konto med [!DNL Blob] kan du ange ett behållarnamn för att ange användaråtkomst till den undermapp du väljer. |
| `folderPath` | Sökvägen till mappen som du vill ge åtkomst till. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Blob] är: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

>[!TIP]
>
>När du har skapat en fil kan du inte ändra autentiseringstypen för en [!DNL Blob] basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

The [!DNL Blob] source stöder både anslutningssträng och autentisering med delad åtkomstsignatur (SAS). En SAS-URI (Shared Access Signature) ger säker delegerad behörighet till din [!DNL Blob] konto. Du kan använda SAS för att skapa autentiseringsuppgifter med olika grad av åtkomst, eftersom en SAS-baserad autentisering gör att du kan ange behörigheter, start- och förfallodatum samt villkor för specifika resurser.

Under det här steget kan du även ange vilka undermappar ditt konto ska ha åtkomst till genom att definiera namnet på behållaren och sökvägen till undermappen.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Blob] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

>[!BEGINTABS]

>[!TAB Anslutningssträng]

Följande begäran skapar en basanslutning för [!DNL Blob] med anslutningssträngsbaserad autentisering:

+++Begäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
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

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB SAS URI-autentisering]

Skapa en [!DNL Blob] anslutning med signatur-URI för delad åtkomst, gör en POST-förfrågan till [!DNL Flow Service] API när du anger värden för [!DNL Blob] `sasUri`.

+++Begäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
      "auth": {
          "specName": "SAS URI Authentication",
          "params": {
              "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
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
| `auth.params.connectionString` | Den SAS-URI som krävs för att komma åt data i [!DNL Blob] lagring. The [!DNL Blob] SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | The [!DNL Blob] ID för lagringsanslutningsspecifikation: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++svar

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Blob] anslutning med API:er och ett unikt ID erhölls som en del av svarstexten. Du kan använda detta anslutnings-ID för att [utforska molnlagring med API:t för Flow Service](../../explore/cloud-storage.md).
