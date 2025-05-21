---
title: Anslut MariaDB till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter ditt MariaDB-konto till Experience Platform med API:er.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Anslut [!DNL MariaDB] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL MariaDB]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL MariaDB] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL MariaDB] översikten](../../../../connectors/databases/mariadb.md#prerequisites) om du vill ha information om autentisering.

### Använda Experience Platform API:er

Läs guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md) om du vill ha information om hur du kan anropa Experience Platform API:er.

## Anslut [!DNL MariaDB] till Experience Platform

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL MariaDB]-konto till Experience Platform.

### Skapa en basanslutning för [!DNL MariaDB]

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

**API-format**

```https
POST /connections
```

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger autentiseringsuppgifterna för ditt [!DNL MariaDB]-konto.

>[!BEGINTABS]

>[!TAB Anslutningssträngsbaserad autentisering]

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL MariaDB]-källa med anslutningssträngsbaserad autentisering.

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som är associerad med din [!DNL MariaDB]-autentisering. Anslutningssträngsmönstret [!DNL MariaDB] är: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL MariaDB] är: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svarsexempel

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB Grundläggande autentisering]

**Begäran**

Följande begäran skapar en basanslutning för en [!DNL MariaDB]-källa med grundläggande autentisering.

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
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.server` | Namnet eller IP-adressen för din [!DNL MariaDB]-databas. |
| `auth.params.database` | Namnet på databasen. |
| `auth.params.username` | Användarnamnet som motsvarar databasen. |
| `auth.params.password` | Lösenordet som motsvarar databasen. |
| `auth.params.sslMode` | Den metod som används för att kryptera data under dataöverföring. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL MariaDB] är: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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

>[!ENDTABS]


## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL MariaDB]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
