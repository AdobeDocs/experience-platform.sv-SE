---
keywords: Experience Platform;hem;populära ämnen;generisk REST;allmän rest
solution: Experience Platform
title: Skapa en allmän REST API-basanslutning med API:t för Flow Service
type: Tutorial
description: Lär dig hur du ansluter allmänt REST API till Adobe Experience Platform med API:t för Flow Service.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# Skapa en allmän REST API-basanslutning med API:t [!DNL Flow Service]

>[!NOTE]
>
>Källan [!DNL Generic REST API] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudien får du hjälp med att skapa en basanslutning för [!DNL Generic REST API] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

### Samla in nödvändiga inloggningsuppgifter

För att [!DNL Flow Service] ska kunna ansluta till [!DNL Generic REST API] måste du ange giltiga autentiseringsuppgifter för den autentiseringstyp som du väljer. [!DNL Generic REST API] har stöd för både OAuth 2-uppdateringskod och grundläggande autentisering. I följande tabeller finns information om autentiseringsuppgifter för de två autentiseringstyper som stöds.

#### OAuth 2-uppdateringskod

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `host` | Värd-URL:en för källan som du begär från. Det här värdet är obligatoriskt och kan inte kringgås med `requestParameterOverride`. |
| `authorizationTestUrl` | (Valfritt) URL:en för auktoriseringstestet används för att validera autentiseringsuppgifter när en basanslutning skapas. Om inget anges kontrolleras autentiseringsuppgifterna automatiskt när du skapar en källanslutning i stället. |
| `clientId` | (Valfritt) Det klient-ID som är kopplat till ditt användarkonto. |
| `clientSecret` | (Valfritt) Klienthemligheten som är kopplad till ditt användarkonto. |
| `accessToken` | Den primära autentiseringsreferens som används för att komma åt programmet. Åtkomsttoken representerar behörigheten för ditt program, för åtkomst till vissa aspekter av en användares data. Det här värdet är obligatoriskt och kan inte kringgås med `requestParameterOverride`. |
| `refreshToken` | (Valfritt) En token som används för att generera en ny åtkomsttoken när åtkomsttoken har upphört att gälla. |
| `expirationDate` | (Valfritt) Ett dolt värde som definierar förfallodatumet för din åtkomsttoken. |
| `accessTokenUrl` | (Valfritt) URL-slutpunkten som används för att hämta din åtkomsttoken. |
| `requestParameterOverride` | (Valfritt) En egenskap som gör att du kan ange vilka autentiseringsparametrar som ska åsidosättas. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Generic REST API] är: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Grundläggande autentisering

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `host` | Värd-URL:en för källan som du begär från. |
| `username` | Användarnamnet som motsvarar ditt användarkonto. |
| `password` | Lösenordet som motsvarar ditt användarkonto. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Generic REST API] är: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

[!DNL Generic REST API] har stöd för både grundläggande autentisering och OAuth 2-uppdateringskod. I följande exempel finns vägledning om hur du autentiserar med någon av autentiseringstyperna.

### Skapa en [!DNL Generic REST API]-basanslutning med OAuth 2-uppdateringskod

Om du vill skapa ett basanslutnings-ID med OAuth 2-uppdateringskod gör du en POST-begäran till `/connections`-slutpunkten och anger dina OAuth 2-autentiseringsuppgifter.

**API-format**

```http
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Egenskap | Beskrivning |
| --------- | ----------- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet på din basanslutning är beskrivande, eftersom du kan använda detta för att söka efter information om din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan inkludera för att få mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som är associerat med [!DNL Generic REST API]. Detta fasta ID är: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Autentiseringstypen som du använder för att autentisera källan till Experience Platform. |
| `auth.params.host` | Den rot-URL som används för att ansluta till din [!DNL Generic REST API]-källa. |
| `auth.params.accessToken` | Motsvarande åtkomsttoken som används för att autentisera källan. Detta krävs för OAuth-baserad autentisering. |

**Svar**

Ett svar returnerar den nyligen skapade anslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att utforska dina data i nästa självstudiekurs.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Skapa en [!DNL Generic REST API]-basanslutning med grundläggande autentisering

Om du vill skapa en [!DNL Generic REST API]-basanslutning med grundläggande autentisering, gör du en POST-begäran till `/connections`-slutpunkten för [!DNL Flow Service] API samtidigt som du anger dina grundläggande autentiseringsuppgifter.

**API-format**

```https
POST /connections
```

**Begäran**

Följande begäran skapar en basanslutning för [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på din basanslutning. Kontrollera att namnet på din basanslutning är beskrivande, eftersom du kan använda detta för att söka efter information om din basanslutning. |
| `description` | (Valfritt) En egenskap som du kan inkludera för att få mer information om din basanslutning. |
| `connectionSpec.id` | Anslutningsspecifikations-ID som är associerat med [!DNL Generic REST API]. Detta fasta ID är: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Autentiseringstypen som du använder för att ansluta källan till Experience Platform. |
| `auth.params.host` | Den rot-URL som används för att ansluta till din [!DNL Generic REST API]-källa. |
| `auth.params.username` | Användarnamnet som motsvarar källan [!DNL Generic REST API]. Detta krävs för grundläggande autentisering. |
| `auth.params.password` | Lösenordet som motsvarar din [!DNL Generic REST API]-källa. Detta krävs för grundläggande autentisering. |

**Svar**

Ett svar returnerar den nyskapade basanslutningen, inklusive dess unika anslutnings-ID (`id`). Detta ID krävs för att undersöka källans filstruktur och innehåll i nästa steg.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Generic REST API]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta protokolldata till Experience Platform med  [!DNL Flow Service] API](../../collect/protocols.md)
