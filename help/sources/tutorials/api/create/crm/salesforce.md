---
title: Anslut Salesforce till Experience Platform med API:t för flödestjänsten
description: Lär dig hur du ansluter Adobe Experience Platform till ett Salesforce-konto med API:t för Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 01f655df8679383f57d60796be5274acd9b5df68
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---

# Anslut [!DNL Salesforce] till Experience Platform med API:t [!DNL Flow Service]

Läs den här vägledningen när du vill veta hur du kan ansluta ditt [!DNL Salesforce]-källkonto till Adobe Experience Platform med [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): [!DNL Experience Platform] tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

### Använda plattforms-API:er

Mer information om hur du kan anropa plattforms-API:er finns i guiden [Komma igång med plattforms-API:er](../../../../../landing/api-guide.md).

## Anslut [!DNL Salesforce] till Experience Platform på [!DNL Azure] {#azure}

Läs stegen nedan om du vill ha information om hur du ansluter [!DNL Salesforce]-källan till Experience Platform på [!DNL Azure].

### Samla in nödvändiga inloggningsuppgifter

Källan [!DNL Salesforce] stöder grundläggande autentisering och autentiseringsuppgifter för OAuth2-klient.

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

Om du vill ansluta ditt [!DNL Salesforce]-konto till [!DNL Flow Service] med grundläggande autentisering anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce]-källinstansen. Formatet för `environmentUrl` är `https://[domain].my.salesforce.com`. |
| `username` | Användarnamnet för användarkontot [!DNL Salesforce]. |
| `password` | Lösenordet för användarkontot [!DNL Salesforce]. |
| `securityToken` | Säkerhetstoken för användarkontot [!DNL Salesforce]. |
| `apiVersion` | Valfritt) REST API-versionen för den [!DNL Salesforce]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du kommer igång finns i [det här Salesforce-dokumentet](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

Om du vill ansluta ditt [!DNL Salesforce]-konto till [!DNL Flow Service] med OAuth 2-klientautentiseringsuppgifter anger du värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `environmentUrl` | URL:en för [!DNL Salesforce]-källinstansen. Formatet för `environmentUrl` är `https://[domain].my.salesforce.com` |
| `clientId` | Klient-ID används tillsammans med klienthemligheten som en del av OAuth2-autentisering. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce]. |
| `clientSecret` | Klienthemligheten används tillsammans med klient-ID som en del av OAuth2-autentiseringen. Tillsammans gör klient-ID och klienthemlighet att ditt program kan fungera för ditt kontos räkning genom att identifiera ditt program för [!DNL Salesforce]. |
| `apiVersion` | REST API-versionen för den [!DNL Salesforce]-instans som du använder. Värdet för API-versionen måste formateras med ett decimaltecken. Om du till exempel använder API-version `52` måste du ange värdet som `52.0`. Om det här fältet lämnas tomt kommer Experience Platform automatiskt att använda den senaste tillgängliga versionen. Det här värdet är obligatoriskt för autentisering av OAuth2-klientautentiseringsuppgifter. |
| `connectionSpec.id` | Anslutningsspecifikationen returnerar en källas kopplingsegenskaper, inklusive autentiseringsspecifikationer för att skapa bas- och källanslutningarna. Anslutningsspecifikations-ID för [!DNL Salesforce] är: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Mer information om hur du använder OAuth för [!DNL Salesforce] finns i [[!DNL Salesforce] handboken om OAuth-auktoriseringsflöden](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Skapa en basanslutning för [!DNL Salesforce] i Experience Platform på [!DNL Azure]

En basanslutning bevarar information mellan källan och plattformen, inklusive källans autentiseringsuppgifter, anslutningsstatus och ditt unika basanslutnings-ID. Med det grundläggande anslutnings-ID:t kan du utforska och navigera bland filer inifrån källan och identifiera de specifika objekt som du vill importera, inklusive information om deras datatyper och format.

Om du vill skapa en basanslutning och ansluta ditt [!DNL Salesforce]-konto till Experience Platform på [!DNL Azure] gör du en POST-förfrågan till `/connections`-slutpunkten och anger dina [!DNL Salesforce] autentiseringsuppgifter i begärandetexten.

**API-format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Grundläggande autentisering]

+++Begäran

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
| `auth.params.environmentUrl` | URL:en för din [!DNL Salesforce]-instans. |
| `auth.params.username` | Användarnamnet som är associerat med ditt [!DNL Salesforce]-konto. |
| `auth.params.password` | Lösenordet som är kopplat till ditt [!DNL Salesforce]-konto. |
| `auth.params.securityToken` | Säkerhetstoken som är associerad med ditt [!DNL Salesforce]-konto. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++

+++svar

Ett lyckat svar returnerar din nyskapade basanslutning tillsammans med dess unika ID.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB Autentiseringsuppgifter för OAuth 2-klient]

+++Begäran

Följande begäran skapar en basanslutning för [!DNL Salesforce] med hjälp av autentiseringsuppgifter för OAuth 2-klient:

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
| `auth.params.environmentUrl` | URL:en för din [!DNL Salesforce]-instans. |
| `auth.params.clientId` | Klient-ID som är associerat med ditt [!DNL Salesforce]-konto. |
| `auth.params.clientSecret` | Klienthemligheten som är associerad med ditt [!DNL Salesforce]-konto. |
| `auth.params.apiVersion` | REST API-versionen för den [!DNL Salesforce]-instans som du använder. |
| `connectionSpec.id` | Anslutningsspecifikations-ID [!DNL Salesforce]: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

+++


+++svar

Ett lyckat svar returnerar din nyskapade basanslutning tillsammans med dess unika ID.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Anslut [!DNL Salesforce] till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](../../../../../landing/multi-cloud.md).

Läs stegen nedan om du vill ha information om hur du ansluter din [!DNL Salesforce]-källa till Experience Platform på AWS.

### Förhandskrav

Mer information om hur du konfigurerar ditt [!DNL Salesforce]-konto så att det kan ansluta till Experience Platform på AWS finns i [[!DNL Salesforce] översikten](../../../../connectors/crm/salesforce.md#aws).

### Skapa en basanslutning för [!DNL Salesforce] på Experience Platform på AWS

Om du vill skapa en basanslutning och ansluta ditt [!DNL Salesforce]-konto till Experience Platform på AWS, gör du en POST-förfrågan till `/connections`-slutpunkten och anger lämpliga värden för dina autentiseringsuppgifter.

**API-format**

```http
POST /connections
```

**Begäran**

+++Välj för att visa begäran

Följande begäran skapar en basanslutning för källan [!DNL Salesforce] i Experience Platform på AWS.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Mer information om hur du hämtar [!DNL Salesforce] `jwtToken` finns i guiden [Konfigurera en [!DNL Salesforce] källa att ansluta till Experience Platform på AWS](../../../../connectors/crm/salesforce.md#aws).

+++

**Svar**

+++Välj för att visa svar

Ett lyckat svar returnerar din nyskapade basanslutning tillsammans med dess unika ID.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### Verifiera din anslutningsstatus

Kontrollera anslutningsstatusen genom att göra en GET-förfrågan till slutpunkten `/connections` och ange det grundläggande anslutnings-ID som genererades i skapandet.

**API-format**

```http
GET /connections
```

**Begäran**

+++Välj för att visa begäran

Följande begäran hämtar information för basanslutnings-ID: `3e908d3f-c390-482b-9f44-43d3d4f2eb82`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

>[!BEGINTABS]

>[!TAB Initierar]

+++Markera för att visa svarsexempel

Följande svar visar information om basanslutnings-ID: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` i läget `initializing`.

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB Aktiverad]

+++Markera för att visa svarsexempel

Följande svar visar information om basanslutnings-ID: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` i läget `enabled`.

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en [!DNL Salesforce]-basanslutning med API:t [!DNL Flow Service]. Du kan använda detta grundläggande anslutnings-ID i följande självstudier:

* [Utforska strukturen och innehållet i datatabellerna med hjälp av  [!DNL Flow Service] API](../../explore/tabular.md)
* [Skapa ett dataflöde för att hämta CRM-data till plattformen med hjälp av  [!DNL Flow Service] API](../../collect/crm.md)
