---
description: På den här sidan visas ett exempel på API-anropet som används för att skapa en Adobe Experience Platform Destination SDK för konfiguration av autentiseringsuppgifter.
title: Skapa en konfiguration för autentiseringsuppgifter
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# Skapa en konfiguration för autentiseringsuppgifter

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`.

## När API-slutpunkten `/credentials` ska användas {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall behöver du ***inte*** använda API-slutpunkten `/credentials`. I stället kan du konfigurera autentiseringsinformationen för målet via `customerAuthenticationConfigurations`-parametrarna för slutpunkten `/destinations`.
> 
>Läs [Konfiguration för kundautentisering](../functionality/destination-configuration/customer-authentication.md) om du vill ha mer information om vilka autentiseringstyper som stöds.

Använd den här API-slutpunkten om du bara vill skapa en autentiseringskonfiguration om det finns ett globalt autentiseringssystem mellan Adobe och målplattformen, och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till målet. I det här fallet måste du skapa en autentiseringskonfiguration med API-slutpunkten `/credentials`.

När du använder ett globalt autentiseringssystem måste du ange `"authenticationRule":"PLATFORM_AUTHENTICATION"` i konfigurationen för [målleverans](../functionality/destination-configuration/destination-delivery.md) när du [skapar en ny målkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för autentiseringsuppgifter {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa en autentiseringskonfiguration {#create}

Du kan skapa en ny autentiseringskonfiguration genom att göra en `POST`-begäran till `/authoring/credentials`-slutpunkten.

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

**Skapa en [!DNL Amazon S3] autentiseringskonfiguration**

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
| `accessId` | Sträng | Åtkomst-ID för [!DNL Amazon S3] |
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

>[!TAB Azure Data Lake Storage]

**Skapa en [!DNL Azure Data Lake Storage] autentiseringskonfiguration**

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

**Skapa en [!DNL Azure Blob Storage] autentiseringskonfiguration**

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

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu när du ska använda slutpunkten för autentiseringsuppgifter och hur du konfigurerar en autentiseringsuppgifter med API-slutpunkten `/authoring/credentials` Läs [hur du använder Destination SDK för att konfigurera målet](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
