---
description: Den här sidan innehåller exempel på API-anropet som används för att uppdatera en befintlig autentiseringskonfiguration via Adobe Experience Platform Destination SDK.
title: Uppdatera en konfiguration för autentiseringsuppgifter
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# Uppdatera en konfiguration för autentiseringsuppgifter

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att uppdatera en befintlig autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`.

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

## Uppdatera en konfiguration för autentiseringsuppgifter {#update}

Du kan uppdatera en [befintlig](create-credential-configuration.md)-autentiseringskonfiguration genom att göra en `PUT`-begäran till `/authoring/credentials`-slutpunkten med den uppdaterade nyttolasten.

Om du vill hämta en befintlig autentiseringskonfiguration och dess motsvarande `{INSTANCE_ID}` läser du artikeln om att [hämta en autentiseringskonfiguration](retrieve-credential-configuration.md).

**API-format**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för den autentiseringskonfiguration som du vill uppdatera. Om du vill hämta en befintlig autentiseringskonfiguration och dess motsvarande `{INSTANCE_ID}` går du till [Hämta en autentiseringskonfiguration](retrieve-credential-configuration.md). |

Följande begäranden uppdaterar befintliga autentiseringskonfigurationer, som definieras av parametrarna i nyttolasten.

Välj varje flik nedan för att visa motsvarande nyttolast.

>[!BEGINTABS]

>[!TAB Grundläggande]

**Uppdatera en grundläggande konfiguration för autentiseringsuppgifter**

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade konfigurationen för autentiseringsuppgifter.

+++

>[!TAB Amazon S3]

**Uppdatera en [!DNL Amazon S3] autentiseringskonfiguration**

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade konfigurationen för autentiseringsuppgifter.

+++

>[!TAB SSH]

**Uppdatera en [!DNL SSH] autentiseringskonfiguration**

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `sshKey` | Sträng | [!DNL SSH]-nyckel för [!DNL SFTP] med [!DNL SSH]-autentisering |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade konfigurationen för autentiseringsuppgifter.

+++

>[!TAB Azure Data Lake Storage]

**Uppdatera en [!DNL Azure Data Lake Storage] autentiseringskonfiguration**

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `servicePrincipalId` | Sträng | [!DNL Azure Service Principal]-ID för [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Sträng | [!DNL Azure Service Principal Key] för [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade konfigurationen för autentiseringsuppgifter.

+++

>[!TAB Azure Blob Storage]

**Uppdatera en [!DNL Azure Blob] autentiseringskonfiguration**

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade konfigurationen för autentiseringsuppgifter.

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du uppdaterar en autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`. Läs [om hur du använder Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
