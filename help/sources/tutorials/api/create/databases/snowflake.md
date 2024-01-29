---
title: Skapa en Snowflake-basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till Snowflake med API:t för Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Skapa en [!DNL Snowflake] basanslutning med [!DNL Flow Service] API

>[!IMPORTANT]
>
>The [!DNL Snowflake] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

Använd följande självstudiekurs för att lära dig hur du skapar en basanslutning för [!DNL Snowflake] med [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

Följande avsnitt innehåller ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Snowflake] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för följande autentiseringsegenskaper för att kunna autentisera dina [!DNL Snowflake] källa.

>[!BEGINTABS]

>[!TAB Autentisering av kontonyckel]

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto för olika [!DNL Snowflake] organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information om kontonamn finns i [!DNL Snowflake] dokumentation om [kontoidentifierare](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data överförs till plattformen. |
| `database` | The [!DNL Snowflake] databasen innehåller de data som du vill ta med plattformen. |
| `username` | Användarnamnet för [!DNL Snowflake] konto. |
| `password` | Lösenordet för [!DNL Snowflake] användarkonto. |
| `role` | Den standardroll för åtkomstkontroll som ska användas i [!DNL Snowflake] session. Rollen ska vara en befintlig roll som redan har tilldelats den angivna användaren. Standardrollen är `PUBLIC`. |
| `connectionString` | Anslutningssträngen som används för att ansluta till [!DNL Snowflake] -instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Autentisering med nyckelpar]

Om du vill använda autentisering med nyckelpar måste du generera ett 2 048-bitars RSA-nyckelpar och sedan ange följande värden när du skapar ett konto för [!DNL Snowflake] källa.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `account` | Ett kontonamn identifierar unikt ett konto inom organisationen. I det här fallet måste du unikt identifiera ett konto för olika [!DNL Snowflake] organisationer. Om du vill göra det måste du lägga till ditt organisationsnamn i kontonamnet. Till exempel: `orgname-account_name`. Mer information om kontonamn finns i [!DNL Snowflake] dokumentation om [kontoidentifierare](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Användarnamnet för [!DNL Snowflake] konto. |
| `privateKey` | The [!DNL Base64-]kodad privat nyckel för din [!DNL Snowflake] konto. Du kan generera antingen krypterade eller okrypterade privata nycklar. Om du använder en krypterad privat nyckel måste du även ange en lösenfras för den privata nyckeln vid autentisering mot Experience Platform. |
| `privateKeyPassphrase` | Lösenfrasen för den privata nyckeln är ett extra säkerhetslager som du måste använda när du autentiserar med en krypterad privat nyckel. Du behöver inte ange lösenfrasen om du använder en okrypterad privat nyckel. |
| `database` | The [!DNL Snowflake] databas som innehåller de data som du vill importera till Experience Platform. |
| `warehouse` | The [!DNL Snowflake] dist.lager hanterar frågekörningsprocessen för programmet. Varje [!DNL Snowflake] lagerstället är oberoende av varandra och måste nås individuellt när data förs över till Experience Platform. |

Mer information om dessa värden finns i [[!DNL Snowflake] autentiseringsguide för nyckelpar](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Du måste ange `PREVENT_UNLOAD_TO_INLINE_URL` flagga till `FALSE` för att tillåta att data tas bort från [!DNL Snowflake] databas till Experience Platform.

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Snowflake] autentiseringsuppgifter som en del av begärandetexten.

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
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till [!DNL Snowflake] -instans. Anslutningssträngsmönstret för [!DNL Snowflake] är `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | The [!DNL Snowflake] anslutningsspecifikation-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++svar

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

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
| `auth.params.account` | Namnet på [!DNL Snowflake] konto. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Snowflake] konto. |
| `auth.params.database` | The [!DNL Snowflake] databas från vilken data hämtas. |
| `auth.params.privateKey` | The [!DNL Base64-]kodad krypterad privat nyckel för din [!DNL Snowflake] konto. |
| `auth.params.privateKeyPassphrase` | Lösenfrasen som motsvarar din privata nyckel. |
| `auth.params.warehouse` | The [!DNL Snowflake] lagerställe som du använder. |
| `connectionSpec.id` | The [!DNL Snowflake] anslutningsspecifikation-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++svar

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

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
| `auth.params.account` | Namnet på [!DNL Snowflake] konto. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Snowflake] konto. |
| `auth.params.database` | The [!DNL Snowflake] databas från vilken data hämtas. |
| `auth.params.privateKey` | The [!DNL Base64-]kodad okrypterad privat nyckel för din [!DNL Snowflake] konto. |
| `auth.params.warehouse` | The [!DNL Snowflake] lagerställe som du använder. |
| `connectionSpec.id` | The [!DNL Snowflake] anslutningsspecifikation-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++svar

Ett lyckat svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

Genom att följa den här självstudiekursen har du skapat en [!DNL Snowflake] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till plattformen med [!DNL Flow Service] API](../../collect/database-nosql.md)
