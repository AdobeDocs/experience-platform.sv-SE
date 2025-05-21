---
title: Anslut MySQL till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter MySQL-databasen till Experience Platform med API:er.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: b73ced639100c95f6c62be92d4796a206a688958
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Anslut [!DNL MySQL] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL MySQL]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL MySQL] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL MySQL] översikten](../../../../connectors/databases/mysql.md#prerequisites) om du vill ha information om autentisering.

### Använda Experience Platform API:er

Läs guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

## Anslut [!DNL MySQL] till Experience Platform på Azure {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL MySQL]-konto till Experience Platform på Azure.

### Skapa en basanslutning för [!DNL MySQL] på Experience Platform på Azure {#azure-base}

En basanslutning länkar källan till Experience Platform, lagrar autentiseringsinformation, anslutningsstatus och ett unikt ID. Använd detta ID för att bläddra bland källfiler och identifiera specifika objekt som ska importeras, inklusive deras datatyper och format.

**API-format**

```https
POST /connections
```

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL MySQL]-autentiseringsuppgifter som en del av parametrarna för begäran.

>[!BEGINTABS]

>[!TAB Anslutningssträngsbaserad autentisering]

**Begäran**

Följande begäran skapar en basanslutning för [!DNL MySQL] med anslutningssträngsbaserad autentisering.

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.connectionString` | Anslutningssträngen [!DNL MySQL] som är associerad med ditt konto. Anslutningssträngsmönstret [!DNL MySQL] är: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL MySQL]: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svarsexempel

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB Grundläggande autentisering]

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL MySQL]-källa med grundläggande autentisering.

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
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "DISABLED"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.server` | Namnet eller IP-adressen för din [!DNL MySQL]-databas. |
| `auth.params.database` | Namnet på databasen. |
| `auth.params.username` | Användarnamnet som motsvarar databasen. |
| `auth.params.password` | Lösenordet som motsvarar databasen. |
| `auth.params.sslMode` | Den metod som används för att kryptera data under dataöverföring. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL MySQL] är: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svarsexempel

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Anslut [!DNL MySQL] till Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL MySQL]-konto till Experience Platform på AWS.

### Skapa en basanslutning för [!DNL MySQL] på Experience Platform på AWS {#aws-base}

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL MySQL] att ansluta till Experience Platform på AWS.

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
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "443",
              "database": "mysql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.server` | Namnet eller IP-adressen för din [!DNL MySQL]-databas. |
| `auth.params.database` | Namnet på databasen. |
| `auth.params.username` | Användarnamnet som motsvarar databasen. |
| `auth.params.password` | Lösenordet som motsvarar databasen. |
| `auth.params.sslMode` | Ett booleskt värde som styr om SSL används eller inte, beroende på serverstödet. Den här konfigurationen är som standard `false`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL MySQL] är: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svarsexempel

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Skapa ett dataflöde för [!DNL MySQL] data

Nu när du har anslutit din [!DNL MySQL]-databas kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../collect/database-nosql.md).