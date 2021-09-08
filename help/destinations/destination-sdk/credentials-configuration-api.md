---
description: På den här sidan beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/credentials`.
title: API-åtgärder för slutpunkt för autentiseringsuppgifter
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# API-åtgärder för slutpunkt för autentiseringsuppgifter {#credentials}

>[!IMPORTANT]
>
>**API-slutpunkt**:  `platform.adobe.io/data/core/activation/authoring/credentials`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/credentials`.

## När ska API-slutpunkten `/credentials` användas {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall behöver du *inte* använda API-slutpunkten `/credentials`. Du kan i stället konfigurera autentiseringsinformationen för målet via `customerAuthenticationConfigurations`-parametrarna för `/destinations`-slutpunkten. Läs [Konfiguration av autentiseringsuppgifter](./credentials-configuration.md) om du vill ha mer information.

Använd den här API-slutpunkten och välj `PLATFORM_AUTHENTICATION` i [målkonfigurationen](./destination-configuration.md#destination-delivery) om det finns ett globalt autentiseringssystem mellan Adobe och målet och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till målet. I det här fallet måste du skapa ett autentiseringsobjekt med API-slutpunkten `/credentials`.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Komma igång med API-åtgärder för konfiguration av autentiseringsuppgifter {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa en autentiseringskonfiguration {#create}

Du kan skapa en ny autentiseringskonfiguration genom att göra en POST-förfrågan till `/authoring/credentials`-slutpunkten.

**API-format**


```http
POST /authoring/credentials
```

**Begäran**

Följande begäran skapar en ny autentiseringskonfiguration, konfigurerad med parametrarna som anges i nyttolasten. Nyttolasten nedan innehåller alla parametrar som accepteras av slutpunkten `/authoring/credentials`. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `username` | Sträng | inloggningsanvändarnamn för konfiguration av inloggningsinformation |
| `password` | Sträng | inloggningslösenord för konfiguration av autentiseringsuppgifter |
| `url` | Sträng | URL för auktoriseringsleverantör |
| `clientId` | Sträng | Klient-ID för klient-/programautentiseringsuppgifter |
| `clientSecret` | Sträng | Klienthemlighet för klient-/programautentiseringsuppgifter |
| `accessToken` | Sträng | Åtkomsttoken från auktoriseringsprovidern |
| `expiration` | Sträng | Åtkomsttokenets TTL-värde |
| `refreshToken` | Sträng | Uppdateringstoken från auktoriseringsprovidern |
| `header` | Sträng | Alla huvuden som krävs för auktorisering |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

## Visa autentiseringskonfigurationer {#retrieve-list}

Du kan hämta en lista över alla autentiseringskonfigurationer för din IMS-organisation genom att göra en GET-begäran till `/authoring/credentials`-slutpunkten.

**API-format**


```http
GET /authoring/credentials
```

**Begäran**

Följande begäran hämtar listan med autentiseringskonfigurationer som du har åtkomst till, baserat på konfigurationen för IMS-organisationen och sandlådan.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över de autentiseringsuppgifter som du har åtkomst till, baserat på IMS-organisationens ID och det sandlådenamn som du använde. Ett `instanceId` motsvarar mallen för en autentiseringskonfiguration. Svaret kortas av för att vara kortfattat.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Uppdatera en befintlig autentiseringskonfiguration {#update}

Du kan uppdatera en befintlig autentiseringskonfiguration genom att göra en PUT-begäran till `/authoring/credentials`-slutpunkten och ange instans-ID för den autentiseringskonfiguration som du vill uppdatera. Ange den uppdaterade konfigurationen för autentiseringsuppgifter i anropets brödtext.

**API-format**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för den autentiseringskonfiguration som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar en befintlig autentiseringskonfiguration, konfigurerad med parametrarna i nyttolasten.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```





## Hämta en specifik autentiseringskonfiguration {#get}

Du kan hämta detaljerad information om en specifik autentiseringskonfiguration genom att göra en GET-förfrågan till `/authoring/credentials`-slutpunkten och ange instans-ID för den autentiseringskonfiguration som du vill uppdatera.

**API-format**


```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för den autentiseringskonfiguration du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna autentiseringskonfigurationen.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```


## Ta bort en specifik autentiseringskonfiguration {#delete}

Du kan ta bort den angivna autentiseringskonfigurationen genom att göra en DELETE-begäran till `/authoring/credentials`-slutpunkten och ange ID:t för den autentiseringskonfiguration du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` för den autentiseringskonfiguration du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu när du ska använda referenserna som slutpunkt och hur du konfigurerar en autentiseringsuppgifter med API-slutpunkten `/authoring/credentials` eller `/authoring/destinations`-slutpunkten. Läs [hur du använder mål-SDK för att konfigurera ditt mål](./configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
