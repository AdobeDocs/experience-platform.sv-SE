---
title: Skapa en Salesforce Service Cloud-källanslutning med API:t för flödestjänst
description: Lär dig hur du ansluter Adobe Experience Platform till Salesforce Service Cloud med API:t för flödestjänst.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Skapa en [!DNL Salesforce Service Cloud] källanslutning med [!DNL Flow Service] API

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

Läs den här självstudiekursen för att lära dig hur du skapar en basanslutning för [!DNL Salesforce Service Cloud] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Service Cloud] med [!DNL Flow Service] API.

### Samla in nödvändiga inloggningsuppgifter

The [!DNL Salesforce Service Cloud] source stöder grundläggande autentisering och OAuth2-klientautentiseringsuppgifter.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Koppla samman [!DNL Salesforce Service Cloud] konto till [!DNL Flow Service] med grundläggande autentisering anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce Service Cloud] källinstans. |
| `username` | Användarnamnet för [!DNL Salesforce Service Cloud] användarkonto. |
| `password` | Lösenordet för [!DNL Salesforce Service Cloud] användarkonto. |
| `securityToken` | Säkerhetstoken för [!DNL Salesforce Service Cloud] användarkonto. |
| `apiVersion` | (Valfritt) REST API-versionen av [!DNL Salesforce Service Cloud] -instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52`måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du kommer igång finns på [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

Koppla samman [!DNL Salesforce Service Cloud] konto till [!DNL Flow Service] Ange värden för följande autentiseringsuppgifter med hjälp av OAuth 2-klientautentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce Service Cloud] källinstans. |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av OAuth2-autentisering. Tillsammans möjliggör klient-ID och klienthemlighet att ditt program arbetar för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av OAuth2-autentiseringen. Tillsammans möjliggör klient-ID och klienthemlighet att ditt program arbetar för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| `apiVersion` | REST API-versionen av [!DNL Salesforce Service Cloud] -instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52`måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. Det här värdet är obligatoriskt för autentisering av OAuth2-klientautentiseringsuppgifter. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om OAuth för [!DNL Salesforce Service Cloud], läsa [[!DNL Salesforce Service Cloud] guide om OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Använda plattforms-API:er

Mer information om hur du kan anropa API:er för plattformar finns i handboken [komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST till `/connections` slutpunkt när du ger [!DNL Salesforce Service Cloud] autentiseringsuppgifter som en del av parametrarna för begäran.

**API-format**

```http
POST /connections
```

**Begäran**

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Följande begäran skapar en basanslutning för [!DNL Salesforce Service Cloud] med grundläggande autentisering:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parameter | Beskrivning |
| ---| --- |
| `auth.params.environmentUrl` | URL:en till [!DNL Salesforce Service Cloud] -instans. |
| `auth.params.username` | Användarnamnet som är associerat med din [!DNL Salesforce Service Cloud] konto. |
| `auth.params.password` | Lösenordet som är kopplat till [!DNL Salesforce Service Cloud] konto. |
| `auth.params.securityToken` | Säkerhetstoken som är kopplad till din [!DNL Salesforce Service Cloud] konto. |
| `connectionSpec.id` | The [!DNL Salesforce Service Cloud] anslutningsspecifikation-ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Autentiseringsuppgifter för OAuth2-klient]

Följande begäran skapar en basanslutning för [!DNL Salesforce Service Cloud] med OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
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
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `auth.params.environmentUrl` | URL:en till [!DNL Salesforce Service Cloud] -instans. |
| `auth.params.clientId` | Klient-ID som är kopplat till din [!DNL Salesforce Service Cloud] konto. |
| `auth.params.clientSecret` | Klienthemligheten som är kopplad till din [!DNL Salesforce Service Cloud] konto. |
| `auth.params.apiVersion` | REST API-versionen av [!DNL Salesforce Service Cloud] -instans som du använder. |
| `connectionSpec.id` | The [!DNL Salesforce Service Cloud] anslutningsspecifikation-ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Svar**

Ett lyckat svar returnerar din nyskapade basanslutning tillsammans med dess unika ID.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce Service Cloud] basanslutning med [!DNL Flow Service] API. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att ta fram data om kundframgångar på plattformen med [!DNL Flow Service] API](../../collect/customer-success.md)
