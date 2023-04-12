---
description: På den här sidan beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/credentials`.
title: API-åtgärder för slutpunkt för autentiseringsuppgifter
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 2%

---

# API-åtgärder för slutpunkt för autentiseringsuppgifter {#credentials}

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med `/authoring/credentials` API-slutpunkt.

En beskrivning av de funktioner som stöds av den här slutpunkten finns i:

* [Konfiguration för direktuppspelningsmål](destination-configuration.md) för de funktioner du kan konfigurera för direktuppspelningsmål.
* [Filbaserad målkonfiguration](file-based-destination-configuration.md) för de funktioner du kan konfigurera för filbaserade mål.

## När ska du använda `/credentials` API-slutpunkt {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall *inte* måste du använda `/credentials` API-slutpunkt. I stället kan du konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt. Läs [Autentiseringskonfiguration](./authentication-configuration.md#when-to-use) för mer information.

Använd den här API-slutpunkten och välj `PLATFORM_AUTHENTICATION` i [målkonfiguration](./destination-configuration.md#destination-delivery) om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med `/credentials` API-slutpunkt.

## Komma igång med API-åtgärder för konfiguration av autentiseringsuppgifter {#get-started}

Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa en autentiseringskonfiguration {#create}

Du kan skapa en ny autentiseringskonfiguration genom att göra en POST-förfrågan till `/authoring/credentials` slutpunkt.

**API-format**

```http
POST /authoring/credentials
```

**Begäran**

Följande begäran skapar en ny autentiseringskonfiguration, konfigurerad med parametrarna som anges i nyttolasten. Nedan finns alla parametrar som accepteras av `/authoring/credentials` slutpunkt. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `username` | Sträng | Inloggningsanvändarnamn för konfiguration av autentiseringsuppgifter |
| `password` | Sträng | Inloggningslösenord för konfiguration av autentiseringsuppgifter |
| `url` | Sträng | URL för auktoriseringsleverantör |
| `clientId` | Sträng | Klient-ID för klient-/programautentiseringsuppgifter |
| `clientSecret` | Sträng | Klienthemlighet för klient-/programautentiseringsuppgifter |
| `accessToken` | Sträng | Åtkomsttoken från auktoriseringsprovidern |
| `expiration` | Sträng | Åtkomsttokenets TTL-värde |
| `refreshToken` | Sträng | Uppdateringstoken från auktoriseringsprovidern |
| `header` | Sträng | Alla huvuden som krävs för auktorisering |
| `accessId` | Sträng | Åtkomst-ID för Amazon S3 |
| `secretKey` | Sträng | Amazon S3 hemlig nyckel |
| `sshKey` | Sträng | SSH-nyckel för SFTP med SSH-autentisering |
| `tenant` | Sträng | Klient för Azure Data Lake Storage |
| `servicePrincipalId` | Sträng | Azure Service Principal ID för Azure Data Lake Storage |
| `servicePrincipalKey` | Sträng | Azure Service Principal Key för Azure Data Lake Storage |
| `connectionString` | Sträng | Anslutningssträng för Azure Blob Storage |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

## Visa autentiseringskonfigurationer {#retrieve-list}

Du kan hämta en lista över alla autentiseringskonfigurationer för din organisation genom att göra en GET-förfrågan till `/authoring/credentials` slutpunkt.

**API-format**


```http
GET /authoring/credentials
```

**Begäran**

Följande begäran hämtar listan med autentiseringskonfigurationer som du har åtkomst till, baserat på konfigurationen för organisationen och sandlådan.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över de autentiseringsuppgifter som du har åtkomst till, baserat på det organisations-ID och sandlådenamn som du använde. Ett `instanceId` motsvarar mallen för en autentiseringskonfiguration. Svaret kortas av för att vara kortfattat.

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

Du kan uppdatera en befintlig autentiseringskonfiguration genom att göra en PUT-begäran till `/authoring/credentials` slutpunkt och ange instans-ID för den autentiseringskonfiguration som du vill uppdatera. Ange den uppdaterade konfigurationen för autentiseringsuppgifter i anropets brödtext.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Du kan hämta detaljerad information om en viss konfiguration av autentiseringsuppgifter genom att göra en GET-förfrågan till `/authoring/credentials` slutpunkt och ange instans-ID för den autentiseringskonfiguration som du vill uppdatera.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Du kan ta bort den angivna autentiseringskonfigurationen genom att göra en DELETE-begäran till `/authoring/credentials` slutpunkt och ange ID:t för den autentiseringskonfiguration som du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | The `id` av den autentiseringskonfiguration du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu när du ska använda slutpunkten för autentiseringsuppgifter och hur du ställer in en konfiguration för autentiseringsuppgifter med `/authoring/credentials` API-slutpunkt eller `/authoring/destinations` slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](./configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
