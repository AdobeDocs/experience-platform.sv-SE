---
title: Skapa en Salesforce Service Cloud Source-anslutning med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till Salesforce Service Cloud med API:t för Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Skapa en [!DNL Salesforce Service Cloud]-källanslutning med API:t [!DNL Flow Service]

En basanslutning representerar den autentiserade anslutningen mellan en källa och Adobe Experience Platform.

I den här självstudiekursen får du lära dig hur du skapar en basanslutning för [!DNL Salesforce Service Cloud] med [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av [!DNL Experience Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enskild [!DNL Experience Platform]-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till [!DNL Salesforce Service Cloud] med API:t [!DNL Flow Service].

### Samla in nödvändiga inloggningsuppgifter

>[!WARNING]
>
>Grundläggande autentisering för källan [!DNL Salesforce Service Cloud] kommer att bli inaktuell i januari 2026. Du måste flytta till autentiseringen för OAuth 2-klientautentiseringsuppgifter för att kunna fortsätta använda källan och hämta data från ditt [!DNL Salesforce Service Cloud]-konto till Experience Platform.

Källan [!DNL Salesforce Service Cloud] stöder grundläggande autentisering och autentiseringsuppgifter för OAuth2-klient.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill ansluta ditt [!DNL Salesforce Service Cloud]-konto till [!DNL Flow Service] med grundläggande autentisering anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce Service Cloud]-källinstansen. |
| `username` | Användarnamnet för användarkontot [!DNL Salesforce Service Cloud]. |
| `password` | Lösenordet för användarkontot [!DNL Salesforce Service Cloud]. |
| `securityToken` | Säkerhetstoken för användarkontot [!DNL Salesforce Service Cloud]. |
| `apiVersion` | (Valfritt) REST API-versionen för den [!DNL Salesforce Service Cloud]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du kommer igång finns i [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

Om du vill ansluta ditt [!DNL Salesforce Service Cloud]-konto till [!DNL Flow Service] med OAuth 2-klientautentiseringsuppgifter anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce Service Cloud]-källinstansen. |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av OAuth2-autentisering. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av OAuth2-autentiseringen. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce Service Cloud]. |
| `apiVersion` | REST API-versionen för den [!DNL Salesforce Service Cloud]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. Det här värdet är obligatoriskt för autentisering av OAuth2-klientautentiseringsuppgifter. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce Service Cloud] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du använder OAuth för [!DNL Salesforce Service Cloud] finns i [[!DNL Salesforce Service Cloud] handboken om OAuth-auktoriseringsflöden](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Använda Experience Platform API:er

Information om hur du kan anropa Experience Platform API:er finns i guiden [Komma igång med Experience Platform API:er](../../../../../landing/api-guide.md).

## Skapa en basanslutning

En basanslutning bevarar information mellan källan och Experience Platform, inklusive autentiseringsuppgifter för källan, anslutningens aktuella tillstånd och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa ett basanslutnings-ID skickar du en POST-begäran till `/connections`-slutpunkten och anger dina [!DNL Salesforce Service Cloud]-autentiseringsuppgifter som en del av parametrarna för begäran.

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
| `auth.params.environmentUrl` | URL:en för din [!DNL Salesforce Service Cloud]-instans. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.securityToken` | Säkerhetstoken som är associerad med ditt [!DNL Salesforce Service Cloud]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB Autentiseringsuppgifter för OAuth2-klient]

Följande begäran skapar en basanslutning för [!DNL Salesforce Service Cloud] med hjälp av autentiseringsuppgifter för OAuth 2-klient:

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
| `auth.params.environmentUrl` | URL:en för din [!DNL Salesforce Service Cloud]-instans. |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce Service Cloud]-konto. |
| `auth.params.apiVersion` | REST API-versionen för den [!DNL Salesforce Service Cloud]-instans som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

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

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce Service Cloud]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att skicka kunddata till Experience Platform med hjälp av  [!DNL Flow Service] API](../../collect/customer-success.md)
