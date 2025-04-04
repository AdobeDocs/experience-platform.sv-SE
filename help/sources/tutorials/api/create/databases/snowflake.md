---
title: Anslut Snowflake till Experience Platform med API:t för flödestjänst
description: Lär dig hur du ansluter Adobe Experience Platform till Snowflake med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

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

## Anslut [!DNL Snowflake] till Experience Platform på Azure {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Snowflake]-källa till Experience Platform på Azure.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsegenskaper för att autentisera [!DNL Snowflake]-källan.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |
| `database` | Databasen [!DNL Snowflake] innehåller de data som du vill hämta Experience Platform. |
| `username` | Användarnamnet för kontot [!DNL Snowflake]. |
| `password` | Lösenordet för användarkontot [!DNL Snowflake]. |
| `role` | Standardrollen för åtkomstkontroll som ska användas i sessionen [!DNL Snowflake]. Rollen ska vara en befintlig roll som redan har tilldelats den angivna användaren. Standardrollen är `PUBLIC`. |
| `connectionString` | Anslutningssträngen som används för att ansluta till din [!DNL Snowflake]-instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autentisering med nyckelpar]

Om du vill använda autentisering med nyckelpar måste du generera ett 2 048-bitars RSA-nyckelpar och sedan ange följande värden när du skapar ett konto för [!DNL Snowflake]-källan.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto i olika [!DNL Snowflake]-organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Läs guiden om att [hämta din [!DNL Snowflake] kontoidentifierare](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) om du vill ha mer information. Mer information finns i [[!DNL Snowflake] dokumentationen](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för ditt [!DNL Snowflake]-konto. |
| `privateKey` | Den [!DNL Base64-]kodade privata nyckeln för ditt [!DNL Snowflake]-konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. Läs guiden om att [hämta din [!DNL Snowflake] privata nyckel](../../../../connectors/databases/snowflake.md) om du vill ha mer information. |
| `privateKeyPassphrase` | Lösenfrasen för den privata nyckeln är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| `database` | Databasen [!DNL Snowflake] som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | Lagerstället [!DNL Snowflake] hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake]-lagerställe är oberoende av varandra och måste nås individuellt när data överförs till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguiden för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

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

+++svar

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

+++svar

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

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
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
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

+++svar

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

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

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Snowflake] som ska importera datum till Experience Platform på AWS:

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

**Svar**

Ett lyckat svar returnerar information om den nyligen skapade anslutningen, inklusive dess unika identifierare (`id`). Detta ID krävs för att du ska kunna utforska ditt lagringsutrymme i nästa självstudiekurs.

+++Markera för att visa exempel

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

Genom att följa den här självstudiekursen har du skapat en [!DNL Snowflake]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
