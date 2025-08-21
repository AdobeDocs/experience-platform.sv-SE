---
title: Anslut Azure Blob Storage till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter Adobe Experience Platform till Azure Blob med API:t för Flow Service.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# Anslut [!DNL Azure Blob Storage] till Experience Platform med API:t

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Azure Blobg Storage]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Azure Blob Storage] översikten](../../../../connectors/cloud-storage/blob.md#authentication) om du vill ha information om autentisering.

## Anslut ditt [!DNL Azure Blob Storage]-konto till Experience Platform {#connect}

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL Azure Blob Storage]-konto till Experience Platform.

### Skapa en basanslutning

>[!NOTE]
>
>När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Azure Blob Storage]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

En basanslutning länkar källan till Experience Platform, lagrar autentiseringsinformation, anslutningsstatus och ett unikt ID. Använd detta ID för att bläddra bland källfiler och identifiera specifika objekt som ska importeras, inklusive deras datatyper och format.

Du kan ansluta ditt [!DNL Azure Blob Storage]-konto till Experience Platform med följande autentiseringstyper:

* **Verifiering av kontonyckel**: Lagringskontots åtkomstnyckel används för att autentisera och ansluta till ditt [!DNL Azure Blob Storage]-konto.
* **Delad åtkomstsignatur (SAS)**: Använder en SAS-URI för att ge delegerad, tidsbegränsad åtkomst till resurser i ditt [!DNL Azure Blob Storage]-konto.
* **Tjänsthuvudbaserad autentisering**: Använder ett Azure Active Directory-tjänstens huvudnamn (AAD) (klient-ID och hemlighet) för att autentisera på ditt Azure Blob Storage-konto på ett säkert sätt.

**API-format**

```https
POST /connections
```

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till slutpunkten `/connections` och anger dina autentiseringsuppgifter som en del av parametrarna för begäran.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

Ange värden för `connectionString`, `container` och `folderPath` om du vill använda kontonyckelautentisering.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
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

| Parameter | Beskrivning |
| --- | --- |
| `connectionString` | Anslutningssträngen för ditt [!DNL Azure Blob Storage]-konto. Anslutningssträngsmönstret är: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | Namnet på behållaren [!DNL Azure Blob Storage] där dina datafiler lagras. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. |
| `connectionSpec.id` | Anslutningens spec-ID för källan [!DNL Azure Blob Storage]. Detta ID har korrigerats som: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Delad åtkomstsignatur]

Om du vill använda signatur för delad åtkomst anger du värden för `sasUri`, `container` och `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
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

| Parameter | Beskrivning |
| --- | --- |
| `sasUri` | Den URI för signatur för delad åtkomst som du kan använda som en alternativ autentiseringstyp för att ansluta ditt konto. SAS URI-mönstret är: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | Namnet på behållaren [!DNL Azure Blob Storage] där dina datafiler lagras. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. |
| `connectionSpec.id` | Anslutningens spec-ID för källan [!DNL Azure Blob Storage]. Detta ID har korrigerats som: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Tjänstens huvudbaserade autentisering]

Om du vill ansluta via huvudbaserad autentisering anger du värden för: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` och `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
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

| Parameter | Beskrivning |
| --- | --- |
| `serviceEndpoint` | Slutpunkts-URL för ditt [!DNL Azure Blob Storage]-konto. Vanligtvis i formatet: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | Klient-/program-ID för Azure Active Directory-tjänstens huvudnamn (AAD) som används för autentisering. |
| `servicePrincipalKey` | Klienthemligheten eller lösenordet som är associerat med Azure-tjänstens huvudnamn. |
| `accountKind` | Typen för ditt [!DNL Azure Blob Storage]-konto. Vanliga värden är `Storage` (allmänt syfte V1), `StorageV2` (allmänt syfte V2), `BlobStorage` och `BlockBlobStorage`. |
| `tenant` | Klient-ID för Azure Active Directory (AAD) där tjänstens huvudnamn är registrerat. |
| `container` | Namnet på behållaren [!DNL Azure Blob Storage] där dina datafiler lagras. |
| `folderPath` | Sökvägen inom den angivna behållaren där filerna finns. |
| `connectionSpec.id` | Anslutningens spec-ID för källan [!DNL Azure Blob Storage]. Detta ID har korrigerats som: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs i nästa steg för att skapa en källanslutning.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Blob]-anslutning med API:er och ett unikt ID har hämtats som en del av svarstexten. Du kan använda det här anslutnings-ID:t för att [utforska molnlagring med API:t för Flow Service ](../../explore/cloud-storage.md).
