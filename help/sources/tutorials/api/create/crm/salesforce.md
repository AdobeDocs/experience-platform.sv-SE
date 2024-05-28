---
title: Skapa en Salesforce-basanslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till ett Salesforce-konto med API:t för Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# Skapa en [!DNL Salesforce] basanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du hjälp med att skapa en basanslutning för [!DNL Salesforce] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta [!DNL Platform] till [!DNL Salesforce] kontot med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

The [!DNL Salesforce] source stöder grundläggande autentisering och OAuth2-klientautentiseringsuppgifter.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Koppla samman [!DNL Salesforce] konto till [!DNL Flow Service] med grundläggande autentisering anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce] källinstans. |
| `username` | Användarnamnet för [!DNL Salesforce] användarkonto. |
| `password` | Lösenordet för [!DNL Salesforce] användarkonto. |
| `securityToken` | Säkerhetstoken för [!DNL Salesforce] användarkonto. |
| `apiVersion` | Valfritt) REST API-versionen av [!DNL Salesforce] -instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52`måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du kommer igång finns på [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

Koppla samman [!DNL Salesforce] konto till [!DNL Flow Service] Ange värden för följande autentiseringsuppgifter med hjälp av OAuth 2-klientautentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce] källinstans. |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av OAuth2-autentisering. Tillsammans möjliggör klient-ID och klienthemlighet att ditt program arbetar för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce]. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av OAuth2-autentiseringen. Tillsammans möjliggör klient-ID och klienthemlighet att ditt program arbetar för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce]. |
| `apiVersion` | REST API-versionen av [!DNL Salesforce] -instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52`måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. Det här värdet är obligatoriskt för autentisering av OAuth2-klientautentiseringsuppgifter. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om OAuth för [!DNL Salesforce], läsa [[!DNL Salesforce] guide om OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt och ange [!DNL Salesforce] autentiseringsuppgifter i begärandetexten.

**API-format**

```http
POST /connections
```

**Begäran**

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Följande begäran skapar en basanslutning för [!DNL Salesforce] med grundläggande autentisering:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.environmentUrl` | URL:en till [!DNL Salesforce] -instans. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Salesforce] konto. |
| `auth.params.password` | Lösenordet som är kopplat till [!DNL Salesforce] konto. |
| `auth.params.securityToken` | Säkerhetstoken som är kopplad till din [!DNL Salesforce] konto. |
| `connectionSpec.id` | The [!DNL Salesforce] anslutningsspecifikation-ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

Följande begäran skapar en basanslutning för [!DNL Salesforce] med OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.environmentUrl` | URL:en till [!DNL Salesforce] -instans. |
| `auth.params.clientId` | Klient-ID som är kopplat till din [!DNL Salesforce] konto. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till din [!DNL Salesforce] konto. |
| `auth.params.apiVersion` | REST API-versionen av [!DNL Salesforce] -instans som du använder. |
| `connectionSpec.id` | The [!DNL Salesforce] anslutningsspecifikation-ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Svar**

Ett lyckat svar returnerar din nyskapade basanslutning tillsammans med dess unika ID.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med [!DNL Flow Service] API](../../collect/crm.md)
