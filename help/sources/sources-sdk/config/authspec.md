---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera autentiseringsspecifikationer för självbetjäningskällor (Batch SDK)
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Konfigurera autentiseringsspecifikationer för självbetjäningskällor (Batch SDK)

Autentiseringsspecifikationer definierar hur Adobe Experience Platform-användare kan ansluta till din källa.

Arrayen `authSpec` innehåller information om de autentiseringsparametrar som krävs för att ansluta en källa till Experience Platform. Alla angivna källor har stöd för flera olika typer av autentisering.

## Autentiseringsspecifikationer

Självbetjäningskällor (Batch SDK) stöder OAuth 2-uppdateringskoder och grundläggande autentisering. Se tabellerna nedan för vägledning om hur du använder en OAuth 2-uppdateringskod och grundläggande autentisering

### OAuth 2-uppdateringskod

En OAuth2-uppdateringskod ger säker åtkomst till ett program genom att generera en temporär åtkomsttoken och en uppdateringstoken. Åtkomsttoken ger dig säker åtkomst till dina resurser utan att du behöver ange andra autentiseringsuppgifter, medan uppdateringstoken gör att du kan generera en ny åtkomsttoken när åtkomsttoken upphör att gälla.

+++Visa exempel på en OAuth 2-uppdateringskod

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `authSpec.name` | Visar namnet på autentiseringstypen som stöds. | `oAuth2-refresh-code` |
| `authSpec.type` | Definierar den typ av autentisering som stöds av källan. | `oAuth2-refresh-code` |
| `authSpec.spec` | Innehåller information om autentiseringens schema, datatyp och egenskaper. |
| `authSpec.spec.$schema` | Definierar det schema som används för autentiseringen. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definierar schemats datatyp. | `object` |
| `authSpec.spec.properties` | Innehåller information om de autentiseringsuppgifter som används för autentiseringen. |
| `authSpec.spec.properties.description` | Visar en kort beskrivning av autentiseringsuppgifterna. |
| `authSpec.spec.properties.type` | Definierar autentiseringsuppgifternas datatyp. | `string` |
| `authSpec.spec.properties.clientId` | Klient-ID som är associerat med ditt program. Klient-ID:t används tillsammans med din klienthemlighet för att hämta din åtkomsttoken. |
| `authSpec.spec.properties.clientSecret` | Klienthemligheten som är kopplad till ditt program. Klienthemligheten används tillsammans med ditt klient-ID för att hämta din åtkomsttoken. |
| `authSpec.spec.properties.accessToken` | Åtkomsttoken ger dig säker åtkomst till ditt program. |
| `authSpec.spec.properties.refreshToken` | Uppdateringstoken används för att generera en ny åtkomsttoken när åtkomsttoken upphör att gälla. |
| `authSpec.spec.properties.expirationDate` | Definierar förfallodatumet för åtkomsttoken. |
| `authSpec.spec.properties.refreshTokenUrl` | Den URL som används för att hämta din uppdateringstoken. |
| `authSpec.spec.properties.accessTokenUrl` | Den URL som används för att hämta din uppdateringstoken. |
| `authSpec.spec.properties.requestParameterOverride` | Gör att du kan ange autentiseringsparametrar som ska åsidosättas vid autentisering. |
| `authSpec.spec.required` | Visar de autentiseringsuppgifter som krävs för att autentisera. | `accessToken` |

{style="table-layout:auto"}

+++

### Grundläggande autentisering

Grundläggande autentisering är en autentiseringstyp som gör att du kan komma åt programmet genom att använda en kombination av ditt användarnamn och ditt lösenord för kontot.

+++ Visa exempel på grundläggande autentisering

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `authSpec.name` | Visar namnet på autentiseringstypen som stöds. | `Basic Authentication` |
| `authSpec.type` | Definierar den typ av autentisering som stöds av källan. | `BasicAuthentication` |
| `authSpec.spec` | Innehåller information om autentiseringens schema, datatyp och egenskaper. |
| `authSpec.spec.$schema` | Definierar det schema som används för autentiseringen. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definierar schemats datatyp. | `object` |
| `authSpec.spec.description` | Visar ytterligare information som är specifik för din autentiseringstyp. |
| `authSpec.spec.properties` | Innehåller information om de autentiseringsuppgifter som används för autentiseringen. |
| `authSpec.spec.properties.username` | Det kontoanvändarnamn som är associerat med ditt program. |
| `authSpec.spec.properties.password` | Kontolösenordet som är kopplat till programmet. |
| `authSpec.spec.required` | Anger de fält som krävs som obligatoriska värden som ska infogas i Experience Platform. | `username` |

{style="table-layout:auto"}

+++

### API-nyckelautentisering {#api-key-authentication}

API-nyckelautentisering är en säker metod för att komma åt API:er genom att tillhandahålla en API-nyckel och andra relevanta autentiseringsparametrar i begäranden. Beroende på din specifika API-information kan du skicka API-nyckeln som en del av begärandehuvudet, frågeparametrarna eller brödtexten.

Följande parametrar krävs vanligtvis vid API-nyckelautentisering:

| Parameter | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `host` | string | Nej | Resurs-URL. |
| `authKey1` | string | Ja | Den första autentiseringsnyckeln som krävs för API-åtkomst. Det skickas vanligtvis i begärandehuvudet eller frågeparametrarna. |
| `authKey2` | string | Valfritt | En andra autentiseringsnyckel. Om det behövs används den här nyckeln ofta för att ytterligare validera begäranden. |
| `authKeyN` | string | Valfritt | En ytterligare autentiseringsvariabel som kan användas vid behov, men API:t. |

{style="table-layout:auto"}

+++Visa API-nyckelautentisering

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Autentiseringsbeteende

Du kan använda parametern `restAttributes` för att definiera hur API-nyckeln ska inkluderas i begäran. I exemplet nedan visar attributet `headerParamName` att `X-Auth-Key1` ska skickas som en rubrik.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Varje autentiseringsnyckel (till exempel `authKey1`, `authKey2` osv.) kan kopplas till `restAttributes` för att avgöra hur de skickas som begäranden.

Om `authKey1` har `"headerParamName": "X-Auth-Key1"`. Detta innebär att begärandehuvudet ska innehålla `X-Auth-Key:{YOUR_AUTH_KEY1}`. Dessutom behöver inte nyckelnamnet och `headerParamName` vara samma. Exempel:

* `authKey1` kan ha `headerParamName: X-Custom-Auth-Key`. Detta innebär att begärandehuvudet kommer att använda `X-Custom-Auth-Key` i stället för `authKey1`.
* Omvänt kan `authKey1` ha `headerParamName: authKey1`. Detta innebär att begärans rubriknamn inte ändras.

**Exempel-API-format**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Exempel på autentiseringsspecifikation

Följande är ett exempel på en slutförd autentiseringsspecifikation som använder en [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md)-källa.

+++Visa exempelautentiseringsspecifikation

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

+++

## Nästa steg

När autentiseringsspecifikationerna är ifyllda kan du fortsätta att konfigurera källspecifikationerna för den källa som du vill integrera med Experience Platform. Mer information finns i dokumentet om [konfigurering av källspecifikationer](./sourcespec.md).
