---
description: Den här sidan beskriver de olika OAuth 2-auktoriseringsflöden som stöds av Destinationen SDK och innehåller anvisningar om hur du ställer in OAuth 2-auktorisering för ditt mål.
title: OAuth 2-auktorisering
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 3%

---


# OAuth 2-auktorisering

Destinationen SDK har stöd för flera åtkomstmetoder till ditt mål. Du kan bland annat autentisera till ditt mål med hjälp av [OAuth 2-auktoriseringsramverk](https://tools.ietf.org/html/rfc6749).

Den här sidan beskriver de olika OAuth 2-auktoriseringsflöden som stöds av Destinationen SDK och innehåller anvisningar om hur du ställer in OAuth 2-auktorisering för ditt mål.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Nej |

## Så här lägger du till OAuth 2-auktoriseringsinformation i målkonfigurationen {#how-to-setup}

### Förutsättningar i systemet {#prerequisites}

Som ett första steg måste du skapa en app i ditt system för Adobe Experience Platform, eller på annat sätt registrera Experience Platform i ditt system. Målet är att generera ett klient-ID och en klienthemlighet som behövs för att autentisera Experience Platform mot målet. Som en del av den här konfigurationen i ditt system behöver du omdirigerings-/återanrops-URL:erna för Adobe Experience Platform OAuth 2, som du kan hämta från listan nedan.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>Stegen för att registrera en omdirigerings-/återanrops-URL för Adobe Experience Platform i ditt system krävs bara för [OAuth 2 med auktoriseringskod](#authorization-code) anslagstyp. För de andra två anslagstyper som stöds (lösenord och klientuppgifter) kan du hoppa över det här steget.

I slutet av det här steget bör du ha:
* Ett klient-ID.
* En klienthemlighet;
* AdobeCallback-URL (för auktoriseringskodens medgivande).

### Vad du behöver göra i Destinationen SDK {#to-do-in-destination-sdk}

Om du vill konfigurera OAuth 2-auktorisering för ditt mål i Experience Platform måste du lägga till din OAuth 2-information i dialogrutan [destinationskonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md), under `customerAuthenticationConfigurations` parameter. Se [kundautentisering](../../functionality/destination-configuration/customer-authentication.md) för detaljerade exempel. Specifika anvisningar om vilka fält du måste lägga till i konfigurationsmallen, beroende på din OAuth 2-auktoriseringstyp, finns längre ned på den här sidan.

## OAuth 2-anslagstyper som stöds {#oauth2-grant-types}

Experience Platform stöder de tre OAuth 2-anslagstyperna i tabellen nedan. Om du har en anpassad OAuth 2-konfiguration kan Adobe stödja den med hjälp av anpassade fält i din integrering. Mer information finns i avsnitten för respektive anslagstyp.

>[!IMPORTANT]
>
>* Du anger indataparametrarna enligt instruktionerna i avsnitten nedan. Adobe-interna system ansluter till din plattforms auktoriseringssystem och hämtar utdataparametrar, som används för att autentisera användaren och upprätthålla auktoriseringen till din destination.
>* Indataparametrarna som markeras med fet stil i tabellen är obligatoriska parametrar i OAuth 2-auktoriseringsflödet. De andra parametrarna är valfria. Det finns andra anpassade indataparametrar som inte visas här, men som beskrivs i detalj i avsnitten [Anpassa din OAuth 2-konfiguration](#customize-configuration) och [Uppdatera åtkomsttoken](#access-token-refresh).

| OAuth 2-bidrag | Indata | Utdata |
|---------|----------|---------|
| Auktoriseringskod | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Lösenord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>accessTokenUrl</b></li><li><b>användarnamn</b></li><li><b>lösenord</b></li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Klientautentiseringsuppgifter | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Tabellen ovan visar de fält som används i OAuth 2-standardflöden. Förutom dessa standardfält kan olika partnerintegreringar kräva ytterligare indata och utdata. Adobe har utformat ett flexibelt ramverk för OAuth 2-auktorisering för Destination SDK som kan hantera variationer av det ovanstående standardfältmönstret och samtidigt ha stöd för en mekanism som automatiskt återskapar ogiltiga utdata, som utgångna åtkomsttoken.

Utdata innehåller alltid en åtkomsttoken som används av Experience Platform för att autentisera och upprätthålla behörigheten till ditt mål.

Det system som Adobe har utformat för OAuth 2-auktorisering:
* Stöder alla tre OAuth 2-stipendiaterna samtidigt som de redovisar eventuella variationer i dem, som extra datafält, icke-standard-API-anrop med mera.
* Stöder åtkomsttoken med varierande livstidsvärden, oavsett om det är 90 dagar, 30 minuter eller något annat livstidsvärde som du anger.
* Stöder OAuth 2-auktoriseringsflöden med eller utan uppdateringstoken.

## OAuth 2 med auktoriseringskod {#authorization-code}

Om målet har stöd för ett standard OAuth 2.0 Authorization Code-flöde (läs [RFC-standardspecifikationer](https://tools.ietf.org/html/rfc6749#section-4.1)) eller en variant av det, se de obligatoriska och valfria fälten nedan:

| OAuth 2-bidrag | Indata | Utdata |
|---------|----------|---------|
| Auktoriseringskod | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>authenticationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Om du vill konfigurera den här auktoriseringsmetoden för målet lägger du till följande rader i konfigurationen när du [skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authType` | Sträng | Använd &quot;OAUTH2&quot;. |
| `grant` | Sträng | Använd&quot;OAUTH2_AUTHZATION_CODE&quot;. |
| `accessTokenUrl` | Sträng | URL:en på din sida, som utfärdar åtkomsttoken och, om du vill, uppdaterar token. |
| `authorizationUrl` | Sträng | URL:en till din auktoriseringsserver, där du omdirigerar användaren till ditt program. |
| `refreshTokenUrl` | Sträng | *Valfritt.* URL:en på din sida, som utfärdar uppdateringstoken. Ofta är `refreshTokenUrl` är samma som `accessTokenUrl`. |
| `clientId` | Sträng | Det klient-ID som systemet tilldelar till Adobe Experience Platform. |
| `clientSecret` | Sträng | Klienthemligheten som ditt system tilldelar Adobe Experience Platform. |
| `scope` | Lista över strängar | *Valfritt*. Ange omfattningen för vad åtkomsttoken tillåter Experience Platform att utföra på dina resurser. Exempel: &quot;read, write&quot;. |

{style="table-layout:auto"}

## OAuth 2 med lösenordsbeviljande

För OAuth 2 Password grant (läs [RFC-standardspecifikationer](https://tools.ietf.org/html/rfc6749#section-4.3)), Experience Platform kräver användarens användarnamn och lösenord. I auktoriseringsflödet utbyter Experience Platform dessa autentiseringsuppgifter för en åtkomsttoken och, om så önskas, en uppdateringstoken.
Adobe använder standardindata nedan för att förenkla destinationskonfigurationen, med möjlighet att åsidosätta värden:

| OAuth 2-bidrag | Indata | Utdata |
|---------|----------|---------|
| Lösenord | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>accessTokenUrl</b></li><li><b>användarnamn</b></li><li><b>lösenord</b></li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Du behöver inte lägga till några parametrar för `username` och `password` i konfigurationen nedan. När du lägger till `"grant": "OAUTH2_PASSWORD"` i målkonfigurationen begär systemet att användaren anger ett användarnamn och lösenord i användargränssnittet i Experience Platform när de autentiseras till ditt mål.

Om du vill konfigurera den här auktoriseringsmetoden för målet lägger du till följande rader i konfigurationen när du [skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authType` | Sträng | Använd &quot;OAUTH2&quot;. |
| `grant` | Sträng | Använd&quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Sträng | URL:en på din sida, som utfärdar åtkomsttoken och, om du vill, uppdaterar token. |
| `clientId` | Sträng | Det klient-ID som systemet tilldelar till Adobe Experience Platform. |
| `clientSecret` | Sträng | Klienthemligheten som ditt system tilldelar Adobe Experience Platform. |
| `scope` | Lista över strängar | *Valfritt*. Ange omfattningen för vad åtkomsttoken tillåter Experience Platform att utföra på dina resurser. Exempel: &quot;read, write&quot;. |

{style="table-layout:auto"}

## OAuth 2 med klientautentiseringsuppgifter

Du kan konfigurera autentiseringsuppgifter för OAuth 2-klient (läs [RFC-standardspecifikationer](https://tools.ietf.org/html/rfc6749#section-4.4)), som har stöd för de standardinställningar för in- och utdata som anges nedan. Du kan anpassa värdena. Se [Anpassa din OAuth 2-konfiguration](#customize-configuration) för mer information.

| OAuth 2-bidrag | Indata | Utdata |
|---------|----------|---------|
| Klientautentiseringsuppgifter | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>omfång</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expirresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Om du vill konfigurera den här auktoriseringsmetoden för målet lägger du till följande rader i konfigurationen när du [skapa en målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authType` | Sträng | Använd &quot;OAUTH2&quot;. |
| `grant` | Sträng | Använd&quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Sträng | URL:en till din auktoriseringsserver, som utfärdar en åtkomsttoken och en valfri uppdateringstoken. |
| `refreshTokenUrl` | Sträng | *Valfritt.* URL:en på din sida, som utfärdar uppdateringstoken. Ofta är `refreshTokenUrl` är samma som `accessTokenUrl`. |
| `clientId` | Sträng | Det klient-ID som systemet tilldelar till Adobe Experience Platform. |
| `clientSecret` | Sträng | Klienthemligheten som ditt system tilldelar Adobe Experience Platform. |
| `scope` | Lista över strängar | *Valfritt*. Ange omfattningen för vad åtkomsttoken tillåter Experience Platform att utföra på dina resurser. Exempel: &quot;read, write&quot;. |

{style="table-layout:auto"}

## Anpassa din OAuth 2-konfiguration {#customize-configuration}

De konfigurationer som beskrivs i avsnitten ovan beskriver OAuth 2-standardstipendier. Det system som Adobe har utformat ger dock flexibilitet så att du kan använda anpassade parametrar för alla variationer i OAuth 2-anslaget. Använd knappen `authenticationDataFields` parametrar, vilket visas i exemplen nedan.

### Exempel 1: använda `authenticationDataFields` för att samla in information från auktoriseringssvaret {#example-1}

I det här exemplet har en målplattform uppdateringstoken som upphör att gälla efter en viss tid. I det här fallet skapar partnern `refreshTokenExpiration` anpassat fält för att få giltigheten för uppdateringstoken från `refresh_token_expires_in` i API-svaret.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Exempel 2: använda `authenticationDataFields` för att tillhandahålla en särskild uppdateringstoken {#example-2}

I det här exemplet ställer en partner in sitt mål för att tillhandahålla en särskild uppdateringstoken. Dessutom returneras inte förfallodatumet för åtkomsttoken i API-svaret, vilket innebär att de kan hårdkoda ett standardvärde, i det här fallet 3 600 sekunder.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Exempel 3: Användaren anger klient-ID och klienthemlighet när han/hon konfigurerar målet {#example-3}

I det här exemplet ska du i stället för att skapa ett globalt klient-ID och en klienthemlighet som i avsnittet [Förutsättningar i systemet](#prerequisites)måste kunden ange klient-ID, klienthemlighet och konto-ID (det ID som kunden använder för att logga in på målet)

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Du kan använda följande parametrar i `authenticationDataFields` för att anpassa din OAuth 2-konfiguration:

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authenticationDataFields.name` | Sträng | Namnet på det anpassade fältet. |
| `authenticationDataFields.title` | Sträng | En titel som du kan ange för det anpassade fältet. |
| `authenticationDataFields.description` | Sträng | En beskrivning av det anpassade datafältet som du ställer in. |
| `authenticationDataFields.type` | Sträng | Definierar typen för det anpassade datafältet. <br> Godkända värden: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Boolean | Anger om det anpassade datafältet krävs i auktoriseringsflödet. |
| `authenticationDataFields.format` | Sträng | När du väljer `"format":"password"`, Adobe krypterar värdet i auktoriseringsdatafältet. Vid användning med `"fieldType": "CUSTOMER"`döljer detta även indata i användargränssnittet när användaren skriver i fältet. |
| `authenticationDataFields.fieldType` | Sträng | Anger om indata kommer från partnern (du) eller från användaren när de ställer in målet i Experience Platform. |
| `authenticationDataFields.value` | Sträng. Boolean. Heltal | Värdet för det anpassade datafältet. Värdet matchar den valda typen från `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Sträng | Anger vilket fält från API-svarssökvägen som du refererar till. |

{style="table-layout:auto"}

## Uppdatera åtkomsttoken {#access-token-refresh}

Adobe har utformat ett system som uppdaterar utgångna åtkomsttoken utan att användaren behöver logga in på din plattform igen. Systemet kan generera en ny token så att aktiveringen till destinationen kan fortsätta utan problem för kunden.

Om du vill konfigurera uppdatering av åtkomsttoken kan du behöva konfigurera en mallad HTTP-begäran som tillåter att Adobe får en ny åtkomsttoken med hjälp av en uppdateringstoken. Om åtkomsttoken har upphört att gälla, tar Adobe den mallbaserade begäran som du har angett och lägger till de parametrar som du har angett. Använd `accessTokenRequest` -parameter för att konfigurera en uppdateringsmekanism för åtkomsttoken.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Du kan använda följande parametrar i `accessTokenRequest` för att anpassa din tokenuppdateringsprocess:

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Sträng | Använd `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Sträng | <ul><li>Använd `PEBBLE_V1` om du använder mallar för värdet i `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Använd `NONE` om värdet i fältet `accessTokenRequest.urlBasedDestination.url.value` är en konstant. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Sträng | Den URL som Experience Platform begär åtkomsttoken. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Sträng | <ul><li>Använd `PEBBLE_V1` om du använder mallar för värdena i `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Använd `NONE` om värdet i fältet `accessTokenRequest.httpTemplate.requestBody.value` är en konstant. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Sträng | Använd mallspråk för att anpassa fält i HTTP-begäran till åtkomsttokenslutpunkten. Mer information om hur du använder mallar för att anpassa fält finns i [mallkonventioner](#templating-conventions) -avsnitt. |
| `accessTokenRequest.httpTemplate.httpMethod` | Sträng | Anger den HTTP-metod som används för att anropa åtkomsttoken-slutpunkten. I de flesta fall är värdet `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Sträng | Anger innehållstypen för HTTP-anropet till åtkomsttoken-slutpunkten. <br> Till exempel: `application/x-www-form-urlencoded` eller `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Sträng | Anger om några huvuden ska läggas till i HTTP-anropet till din åtkomsttokenslutpunkt. |
| `accessTokenRequest.responseFields.templatingStrategy` | Sträng | <ul><li>Använd `PEBBLE_V1` om du använder mallar för värdena i `accessTokenRequest.responseFields.value`.</li><li> Använd `NONE` om värdet i fältet `accessTokenRequest.responseFields.value` är en konstant. </li></li> |
| `accessTokenRequest.responseFields.value` | Sträng | Använd mallspråk för att komma åt fält i HTTP-svaret från åtkomsttokenslutpunkten. Mer information om hur du använder mallar för att anpassa fält finns i [mallkonventioner](#templating-conventions) -avsnitt. |
| `accessTokenRequest.validations.name` | Sträng | Anger namnet som du angav för den här valideringen. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Sträng | <ul><li>Använd `PEBBLE_V1` om du använder mallar för värdena i `accessTokenRequest.validations.actualValue.value`.</li><li> Använd `NONE` om värdet i fältet `accessTokenRequest.validations.actualValue.value` är en konstant. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Sträng | Använd mallspråk för att komma åt fält i HTTP-svaret. Mer information om hur du använder mallar för att anpassa fält finns i [mallkonventioner](#templating-conventions) -avsnitt. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Sträng | <ul><li>Använd `PEBBLE_V1` om du använder mallar för värdena i `accessTokenRequest.validations.expectedValue.value`.</li><li> Använd `NONE` om värdet i fältet `accessTokenRequest.validations.expectedValue.value` är en konstant. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Sträng | Använd mallspråk för att komma åt fält i HTTP-svaret. Mer information om hur du använder mallar för att anpassa fält finns i [mallkonventioner](#templating-conventions) -avsnitt. |

{style="table-layout:auto"}

## Mallkonventioner {#templating-conventions}

Beroende på hur du anpassar din behörighet kan du behöva komma åt datafält i auktoriseringssvaret, vilket visas i föregående avsnitt. För att göra det, var vänlig och bekanta dig med [Mallspråk](https://pebbletemplates.io/) som används av Adobe och som hänvisar till mallkonventionerna nedan för att anpassa OAuth 2-implementeringen.


| Prefix | Beskrivning | Exempel |
|---------|----------|---------|
| authData | Få åtkomst till värden i alla partner- och kunddatafält. | ``{{ authData.accessToken }}`` |
| response.body | HTTP-svarsbrödtext | ``{{ response.body.access_token }}`` |
| response.status | HTTP-svarsstatus | ``{{ response.status }}`` |
| response.headers | HTTP-svarsrubriker | ``{{ response.headers.server[0] }}`` |
| userContext | Åtkomstinformation om aktuellt auktoriseringsförsök | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

Genom att läsa den här artikeln får du nu en förståelse för de OAuth 2-autentiseringsmönster som stöds av Adobe Experience Platform och veta hur du konfigurerar ditt mål med OAuth 2-auktoriseringsstöd. Sedan kan du konfigurera ditt mål som stöds av OAuth 2 med Destination SDK. Läs [Använd Destination SDK för att konfigurera ditt mål](../../guides/configure-destination-instructions.md) för nästa steg.
