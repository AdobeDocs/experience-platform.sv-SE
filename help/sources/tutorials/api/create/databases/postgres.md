---
title: Anslut PostgreSQL till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter din [!DNL PostgreSQL] databas till Experience Platform med API:er.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 5348158f6de9fea1a9fe186a14409afb7e7a376e
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Skapa en [!DNL PostgreSQL]-basanslutning med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill lära dig hur du ansluter din [!DNL PostgreSQL]-databas till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL PostgreSQL] med API:t [!DNL Flow Service].

### Använda Experience Platform API:er

Läs guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL PostgreSQL] översikten](../../../../connectors/databases/postgres.md) om du vill ha mer information om autentisering.

### Aktivera SSL-kryptering för anslutningssträngen

Du kan aktivera SSL-kryptering för anslutningssträngen [!DNL PostgreSQL] genom att lägga till anslutningssträngen med följande egenskaper:

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `EncryptionMethod` | Gör att du kan aktivera SSL-kryptering på dina [!DNL PostgreSQL]-data. | <uL><li>`EncryptionMethod=0`(Inaktiverad)</li><li>`EncryptionMethod=1`(Aktiverad)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validerar certifikat som skickas av din [!DNL PostgreSQL]-databas när `EncryptionMethod` används. | <uL><li>`ValidationServerCertificate=0`(Inaktiverad)</li><li>`ValidationServerCertificate=1`(Aktiverad)</li></ul> |

Följande är ett exempel på en [!DNL PostgreSQL]-anslutningssträng med SSL-kryptering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Anslut [!DNL PostgreSQL] till Experience Platform på Azure {#azure}

Läs stegen nedan för att lära dig hur du ansluter ditt [!DNL PostgreSQL]-konto till Experience Platform på Azure.

### Skapa en basanslutning {#azure-base}

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL PostgreSQL]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Kontonyckelbaserad autentisering]

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PostgreSQL] med kontonyckelbaserad autentisering:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| ------------- | --------------- |
| `auth.params.connectionString` | Anslutningssträngen som är associerad med ditt [!DNL PostgreSQL]-konto. Anslutningssträngsmönstret [!DNL PostgreSQL] är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID:n [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyskapade basanslutningen.

+++Visa svarsexempel

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB Grundläggande autentisering]

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PostgreSQL] med grundläggande autentisering:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| ---| --- |
| `auth.params.server` | Namnet eller IP-adressen för din [!DNL PostgreSQL]-databas. |
| `auth.params.port` | Portnumret för databasservern. |
| `auth.params.database` | Namnet på din [!DNL PostgreSQL]-databas. |
| `auth.params.username` | Det användarnamn som är associerat med din [!DNL PostgreSQL]-databasautentisering. |
| `auth.params.password` | Lösenordet som är kopplat till din [!DNL PostgreSQL]-databasautentisering. |
| `auth.params.sslMode` | Den metod som används för att kryptera data under dataöverföring. De tillgängliga värdena är: `Disable`, `Allow`, `Prefer`, `Verify Ca` och `Verify Full`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID:n [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyskapade basanslutningen.

+++Visa svarsexempel

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Anslut [!DNL PostgreSQL] till Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL PostgreSQL]-databas till Experience Platform på AWS.

### Skapa en basanslutning {#aws-base}

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL PostgreSQL]-autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL PostgreSQL] att ansluta till Experience Platform på AWS.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSL_MODE}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| ---| --- |
| `auth.params.server` | Namnet eller IP-adressen för din [!DNL PostgreSQL]-databas. |
| `auth.params.port` | Portnumret för databasservern. |
| `auth.params.database` | Namnet på din [!DNL PostgreSQL]-databas. |
| `auth.params.username` | Det användarnamn som är associerat med din [!DNL PostgreSQL]-databasautentisering. |
| `auth.params.password` | Lösenordet som är kopplat till din [!DNL PostgreSQL]-databasautentisering. |
| `auth.params.sslMode` | Den metod som används för att kryptera data under dataöverföring. De tillgängliga värdena är: `Disable`, `Allow`, `Prefer`, `Verify Ca` och `Verify Full`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID:n [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Svar**

Ett lyckat svar returnerar den unika identifieraren (`id`) för den nyskapade basanslutningen.

+++Visa svarsexempel

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Nästa steg

Nu när du har skapat en anslutning mellan din [!DNL PostgreSQL]-databas och Experience Platform kan du nu gå vidare till nästa steg och överföra dina [!DNL PostgreSQL]-data till Experience Platform. Mer information finns i följande dokumentation:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
