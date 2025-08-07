---
title: Anslut Oracle DB till Experience Platform med API:t för flödestjänsten
description: Lär dig hur du ansluter Oracle DB till Experience Platform med API:er.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Anslut [!DNL Oracle DB] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Oracle DB]-konto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Oracle] med API:t [!DNL Flow Service].

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Oracle DB] översikten](../../../../connectors/databases/oracle.md#prerequisites) om du vill ha information om autentisering.

## Anslut [!DNL Oracle DB] till Experience Platform på Azure {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL Oracle DB]-konto till Experience Platform på Azure.

### Skapa en basanslutning för [!DNL Oracle DB] på Experience Platform på Azure {#azure-base}

En basanslutning länkar källan till Experience Platform, lagrar autentiseringsinformation, anslutningsstatus och ett unikt ID. Använd detta ID för att bläddra bland källfiler och identifiera specifika objekt som ska importeras, inklusive deras datatyper och format.

**API-format**

```https
POST /connections
```

Om du vill skapa ett basanslutnings-ID skapar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Oracle DB]-autentiseringsuppgifter som en del av parametrarna för begäran.

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle DB] med autentisering av anslutningssträngar.

+++Visa begäran


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `auth.params.connectionString` | Anslutningssträngen som används för att ansluta till [!DNL Oracle DB]. Anslutningssträngsmönstret [!DNL Oracle DB] är: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Svar**

Ett godkänt svar returnerar information om den nya basanslutningen, inklusive dess unika identifierare (`id`).

+++Visa svar

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Anslut [!DNL Oracle DB] till Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter ditt [!DNL Oracle DB]-konto till Experience Platform på AWS.

### Skapa en basanslutning för [!DNL Oracle DB] på Experience Platform på AWS {#aws-base}

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Oracle DB] att ansluta till Experience Platform på AWS.

+++Visa begäran

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
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
| `auth.params.server` | IP-adressen eller värdnamnet för [!DNL Oracle DB]-servern. |
| `auth.params.port` | Portnumret för [!DNL Oracle DB]-servern. |
| `auth.params.database` | Namnet på den [!DNL Oracle DB]-instans som du ansluter till. |
| `auth.params.username` | Användarkontot som är associerat med din [!DNL Oracle DB]-instans. |
| `auth.prams.password` | Lösenordet som motsvarar ditt [!DNL Oracle DB]-användarkonto. |
| `auth.params.schema` | Schemat som innehåller databasobjekten. |
| `auth.params.sslMode` | Ett booleskt värde som anger om SSL-mått används eller inte. |
| `connectionSpec.id` | Anslutningens spec-ID som motsvarar källan [!DNL Oracle DB]. Detta ID-värde är fast som: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Svar**

Ett lyckat svar returnerar information om den nyskapade basanslutningen, inklusive dess unika identifierare (`id`) och motsvarande. Du kan använda ID:t för att [skapa en källanslutning](../../collect/database-nosql.md#create-a-source-connection) och `etag` för att [uppdatera ditt konto](../../update.md).

+++Visa svar

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Skapa ett dataflöde för [!DNL Oracle DB] data

Nu när du har anslutit ditt [!DNL Oracle DB]-konto kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../collect/database-nosql.md).