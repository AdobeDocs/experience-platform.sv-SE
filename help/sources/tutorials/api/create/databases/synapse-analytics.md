---
title: Koppla Azure Synapse Analytics till Experience Platform med API:t för Flow Service
description: Lär dig hur du ansluter ditt Azure Synapse Analytics-konto till Experience Platform med API:er.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---

# Anslut [!DNL Azure Synapse Analytics] till Experience Platform med API:t [!DNL Flow Service]

>[!IMPORTANT]
>
>Källan [!DNL Azure Synapse Analytics] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Azure Synapse Analytics]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Azure Synapse Analytics] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Azure Synapse Analytics] översikten](../../../../connectors/databases/synapse-analytics.md#prerequisites) om du vill ha information om autentisering.

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Anslut [!DNL Azure Synapse Analytics] till Experience Platform

Läs följande om du vill veta mer om hur du skapar en basanslutning och ansluter ditt [!DNL Azure Synapse Analytics]-konto till Experience Platform.

### Skapa en basanslutning

En **basanslutning** lagrar nyckelinformation som länkar källsystemet till Adobe Experience Platform. Detta inkluderar:

* Autentiseringsuppgifter för källan
* Anslutningens aktuella status
* Ett unikt **basanslutnings-ID**

Med det **grundläggande anslutnings-ID:t** kan du bläddra bland och utforska filer från din källa, vilket hjälper dig att identifiera vilka objekt som ska importeras samt deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till slutpunkten `/connections`, inklusive dina [!DNL Azure Synapse Analytics] autentiseringsuppgifter i parametrarna för begäran.

**API-format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Anslutningssträngsbaserad autentisering]

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Azure Synapse Analytics] med anslutningssträngsbaserad autentisering.

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
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till [!DNL Azure Synapse Analytics]. Anslutningssträngsmönstret [!DNL Azure Synapse Analytics] är `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Azure Synapse Analytics] är: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa exempelsvar

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Tjänstens huvudnyckelbaserade autentisering]

Följande begäran skapar en basanslutning för [!DNL Azure Synapse Analytics] med huvudnyckelbaserad autentisering för tjänsten.

**Begäran**

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
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `auth.params.server` | Det fullständiga kvalificerade domännamnet för SQL-slutpunkten [!DNL Azure Synapse Analytics]. |
| `auth.params.database` | Namnet på den specifika databasen på arbetsytan för [!DNL Azure Synapse Analytics]. |
| `auth.params.tenant` | Det [!DNL Azure Active Directory]-klientorganisations-ID som är kopplat till din [!DNL Azure]-prenumeration. |
| `auth.params.servicePrincipalId` | Klient-ID för ett [!DNL Azure Active Directory]-program. |
| `auth.params.servicePrincipalKey` | Klienthemligheten eller lösenordet som är kopplat till tjänstens huvudnamn. |
| `connectSpec.id` | Anslutningens spec-ID för [!DNL Azure Synapse Analytics]. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa exempelsvar

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Azure Synapse Analytics]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta databasdata till Experience Platform med  [!DNL Flow Service] API](../../collect/database-nosql.md)
