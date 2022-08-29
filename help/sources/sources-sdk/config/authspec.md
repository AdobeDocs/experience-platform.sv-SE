---
keywords: Experience Platform;hem;populära ämnen;källor;kopplingar;källkopplingar;källor sdk;sdk;SDK
title: Konfigurera autentiseringsspecifikationer för självbetjäningskällor (batch-SDK)
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över de konfigurationer du behöver förbereda för att kunna använda självbetjäningskällor (Batch SDK).
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 25e0061cc47ec4179f3f02958eb8bda1714ea139
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# Konfigurera autentiseringsspecifikationer för självbetjäningskällor (batch-SDK)

Autentiseringsspecifikationer definierar hur Adobe Experience Platform-användare kan ansluta till din källa.

The `authSpec` arrayen innehåller information om de autentiseringsparametrar som krävs för att ansluta en källa till plattformen. Alla angivna källor har stöd för flera olika typer av autentisering.

## Autentiseringsspecifikationer

Självbetjäningskällor (Batch SDK) stöder OAuth 2-uppdateringskoder och grundläggande autentisering. Se tabellerna nedan för vägledning om hur du använder en OAuth 2-uppdateringskod och grundläggande autentisering

### OAuth 2-uppdateringskod

En OAuth2-uppdateringskod ger säker åtkomst till ett program genom att generera en temporär åtkomsttoken och en uppdateringstoken. Åtkomsttoken ger dig säker åtkomst till dina resurser utan att du behöver ange andra autentiseringsuppgifter, medan uppdateringstoken gör att du kan generera en ny åtkomsttoken när åtkomsttoken upphör att gälla.

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

{style=&quot;table-layout:auto&quot;}


### Grundläggande autentisering

Grundläggande autentisering är en autentiseringstyp som gör att du kan komma åt programmet genom att använda en kombination av ditt användarnamn och ditt lösenord för kontot.

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
| `authSpec.spec.required` | Anger de fält som krävs som obligatoriska värden som ska anges i Platform. | `username` |

{style=&quot;table-layout:auto&quot;}

## Exempel på autentiseringsspecifikation

Följande är ett exempel på en slutförd autentiseringsspecifikation som använder en [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) källa.

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

## Nästa steg

När autentiseringsspecifikationerna är ifyllda kan du fortsätta att konfigurera källspecifikationerna för den källa som du vill integrera med plattformen. Se dokumentet på [konfigurera källspecifikationer](./sourcespec.md) för mer information.
