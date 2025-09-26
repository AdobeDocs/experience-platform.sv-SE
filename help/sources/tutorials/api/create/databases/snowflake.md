---
title: Anslut Snowflake till Experience Platform med API:t för flödestjänst
description: Lär dig hur du ansluter Adobe Experience Platform till Snowflake med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# Anslut [!DNL Snowflake] till Experience Platform med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Snowflake] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill veta hur du kan ansluta ditt [!DNL Snowflake]-källkonto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Snowflake] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Snowflake] översikten](../../../../connectors/databases/snowflake.md#prerequisites) om du vill ha information om autentisering.

## Anslut [!DNL Snowflake] till Experience Platform på Azure {#azure}

>[!WARNING]
>
>Grundläggande autentisering (eller kontonyckelautentisering) för källan [!DNL Snowflake] kommer att bli inaktuell i november 2025. Du måste gå över till nyckelparsbaserad autentisering för att kunna fortsätta använda källan och hämta data från din databas till Experience Platform. Mer information om borttagningen finns i [[!DNL Snowflake] metodguiden om bästa praxis för att minska riskerna för kreditvärdighetsförluster](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Snowflake]-källa till Experience Platform på Azure.

>[!NOTE]
>
>Du måste ange flaggan `PREVENT_UNLOAD_TO_INLINE_URL` till `FALSE` för att tillåta dataradering från din [!DNL Snowflake]-databas till Experience Platform.

### Skapa en basanslutning för [!DNL Snowflake] på Experience Platform på Azure {#azure-base}

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Snowflake]-autentiseringsuppgifter som en del av begärandetexten.

**API-format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

+++Begäran

Följande begäran skapar en basanslutning för [!DNL Snowflake]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till din [!DNL Snowflake]-instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Svar

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Autentisering med nyckelpar med krypterad privat nyckel]

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
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.account` | Namnet på ditt [!DNL Snowflake]-konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| `auth.params.database` | Databasen [!DNL Snowflake] från vilken data hämtas. |
| `auth.params.privateKey` | Den [!DNL Base64-]kodade krypterade privata nyckeln för ditt [!DNL Snowflake]-konto. |
| `auth.params.privateKeyPassphrase` | Lösenfrasen som motsvarar din privata nyckel. |
| `auth.params.warehouse` | Det [!DNL Snowflake]-lagerställe som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Autentisering med nyckelpar med okrypterad privat nyckel]

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
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.account` | Namnet på ditt [!DNL Snowflake]-konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| `auth.params.database` | Databasen [!DNL Snowflake] från vilken data hämtas. |
| `auth.params.privateKey` | Den [!DNL Base64-]kodade okrypterade privata nyckeln för ditt [!DNL Snowflake]-konto. |
| `auth.params.warehouse` | Det [!DNL Snowflake]-lagerställe som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Anslut [!DNL Snowflake] till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Snowflake]-källa till Experience Platform på AWS.

### Skapa en basanslutning för [!DNL Snowflake] på Experience Platform i AWS {#aws-base}

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Följande begäran skapar en basanslutning för [!DNL Snowflake] att importera data till Experience Platform på AWS:

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
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.host` | Den värd-URL som ditt [!DNL Snowflake]-konto ansluter till. |
| `auth.params.port` | Portnumret som används av [!DNL Snowflake] vid anslutning till en server via Internet. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| `auth.params.database` | Databasen [!DNL Snowflake] från vilken data hämtas. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Snowflake]-konto. |
| `auth.params.warehouse` | Det [!DNL Snowflake]-lagerställe som du använder. |
| `auth.params.schema` | Namnet på schemat som är associerat med din [!DNL Snowflake]-databas. Du måste se till att användaren som du vill ge databasåtkomst till också har åtkomst till det här schemat. |

+++

+++Svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!TAB Autentisering med nyckelpar med okrypterad privat nyckel]

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
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.account` | Namnet på ditt [!DNL Snowflake]-konto. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Snowflake]-konto. |
| `auth.params.database` | Databasen [!DNL Snowflake] från vilken data hämtas. |
| `auth.params.privateKey` | Den [!DNL Base64-]kodade okrypterade privata nyckeln för ditt [!DNL Snowflake]-konto. |
| `auth.params.warehouse` | Det [!DNL Snowflake]-lagerställe som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Snowflake]: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++


+++Svar

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`).

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

Genom att följa den här självstudiekursen har du skapat en [!DNL Snowflake]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
