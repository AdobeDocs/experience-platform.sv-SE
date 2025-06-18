---
title: Anslut Salesforce Marketing Cloud till Experience Platform med API:t för flödestjänst
description: Lär dig hur du ansluter ditt Salesforce Marketing Cloud-konto till Experience Platform med API:er.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med API:t [!DNL Flow Service]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Salesforce Marketing Cloud]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Azure Synapse Analytics] med API:t [!DNL Flow Service].


### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Marketing Cloud] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Salesforce Marketing Cloud] autentiseringsöversikten](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md) om du vill ha mer information om autentisering.

### Använda Experience Platform API:er

Läs guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform på [!DNL Azure]

Läs följande om du vill veta mer om hur du skapar en basanslutning och ansluter ditt [!DNL Salesforce Marketing Cloud]-konto till Experience Platform på [!DNL Azure].

### Skapa en basanslutning {#azure-base}

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].

En **basanslutning** lagrar nyckelinformation som länkar källsystemet till Adobe Experience Platform. Detta inkluderar:

* Autentiseringsuppgifter för källan
* Anslutningens aktuella status
* Ett unikt **basanslutnings-ID**

Med det **grundläggande anslutnings-ID:t** kan du bläddra bland och utforska filer från din källa, vilket hjälper dig att identifiera vilka objekt som ska importeras samt deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till slutpunkten `/connections`, inklusive dina [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter i parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Salesforce Marketing Cloud].

+++Visa exempelbegäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Marketing Cloud]-program. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Visa exempelsvar

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL Salesforce Marketing Cloud]-konto till Experience Platform på AWS.

### Skapa en basanslutning {#aws-base}

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Salesforce Service Cloud] att ansluta till Experience Platform på AWS.

+++Exempel på visningsbegäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svarsexempel

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Skapa ett dataflöde för [!DNL Salesforce Marketing Cloud] data

Nu när du har anslutit ditt [!DNL Salesforce Marketing Cloud]-konto kan du [skapa ett dataflöde och importera data från din leverantör av marknadsföringsautomatisering till Experience Platform](../../collect/marketing-automation.md).