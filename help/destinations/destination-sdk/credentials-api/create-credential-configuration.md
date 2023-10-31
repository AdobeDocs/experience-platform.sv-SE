---
description: På den här sidan visas ett exempel på API-anropet som används för att skapa en Adobe Experience Platform Destination SDK för konfiguration av autentiseringsuppgifter.
title: Skapa en konfiguration för autentiseringsuppgifter
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 4%

---

# Skapa en konfiguration för autentiseringsuppgifter

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en autentiseringskonfiguration med `/authoring/credentials` API-slutpunkt.

## När ska `/credentials` API-slutpunkt {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall ***inte*** måste du använda `/credentials` API-slutpunkt. I stället kan du konfigurera autentiseringsinformationen för ditt mål via `customerAuthenticationConfigurations` parametrarna för `/destinations` slutpunkt.
> 
>Läs [Konfiguration av kundautentisering](../functionality/destination-configuration/customer-authentication.md) för detaljerad information om vilka autentiseringstyper som stöds.

Använd den här API-slutpunkten om du bara vill skapa en autentiseringskonfiguration om det finns ett globalt autentiseringssystem mellan Adobe och målplattformen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa en autentiseringskonfiguration med `/credentials` API-slutpunkt.

När du använder ett globalt autentiseringssystem måste du ange `"authenticationRule":"PLATFORM_AUTHENTICATION"` i [destinationsleverans](../functionality/destination-configuration/destination-delivery.md) konfiguration, när [skapa en ny målkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för autentiseringsuppgifter {#get-started}

Innan du fortsätter bör du granska [komma igång-guide](../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa en autentiseringskonfiguration {#create}

Du kan skapa en ny konfiguration för autentiseringsuppgifter genom att skapa en `POST` begäran till `/authoring/credentials` slutpunkt.

**API-format**

```http
POST /authoring/credentials
```

Följande begäranden skapar nya autentiseringskonfigurationer, som definieras av parametrarna i nyttolasten.

Välj varje flik nedan för att visa motsvarande nyttolast.

>[!BEGINTABS]

>[!TAB Grundläggande]

**Skapa en grundläggande konfiguration för autentiseringsuppgifter**

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `url` | Sträng | URL för auktoriseringsleverantör |
| `username` | Sträng | Inloggningsanvändarnamn för konfiguration av autentiseringsuppgifter |
| `password` | Sträng | Inloggningslösenord för konfiguration av autentiseringsuppgifter |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

+++

>[!TAB Amazon S3]

**Skapa en [!DNL Amazon S3] konfiguration av autentiseringsuppgifter**

+++**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `accessId` | Sträng | [!DNL Amazon S3] åtkomst-ID |
| `secretKey` | Sträng | [!DNL Amazon S3] hemlig nyckel |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

+++

>[!TAB SSH]

**Skapa en SSH-autentiseringskonfiguration**

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `username` | Sträng | Inloggningsanvändarnamn för konfiguration av autentiseringsuppgifter |
| `sshKey` | Sträng | SSH-nyckel för SFTP med SSH-autentisering |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

+++

>[!TAB Azure Data Lake-lagring]

**Skapa en [!DNL Azure Data Lake Storage] konfiguration av autentiseringsuppgifter**

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `url` | Sträng | URL för auktoriseringsleverantör |
| `tenant` | Sträng | Klient för Azure Data Lake Storage |
| `servicePrincipalId` | Sträng | Azure Service Principal ID för Azure Data Lake Storage |
| `servicePrincipalKey` | Sträng | Azure Service Principal Key för Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

+++

>[!TAB Azure Blob Storage]

**Skapa en [!DNL Azure Blob Storage] konfiguration av autentiseringsuppgifter**

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `connectionString` | Sträng | [!DNL Azure Blob Storage] anslutningssträng |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för dina nya autentiseringsuppgifter.

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu när du ska använda slutpunkten för autentiseringsuppgifter och hur du ställer in en konfiguration för autentiseringsuppgifter med `/authoring/credentials` Läs API-slutpunkt [Så här använder du Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
