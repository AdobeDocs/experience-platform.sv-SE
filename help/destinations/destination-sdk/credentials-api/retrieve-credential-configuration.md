---
description: På den här sidan visas ett exempel på API-anropet som används för att hämta en autentiseringskonfiguration via Adobe Experience Platform Destination SDK.
title: Hämta en konfiguration för autentiseringsuppgifter
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Hämta en konfiguration för autentiseringsuppgifter

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att hämta en autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`.

## När API-slutpunkten `/credentials` ska användas {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall behöver du ***inte*** använda API-slutpunkten `/credentials`. I stället kan du konfigurera autentiseringsinformationen för målet via `customerAuthenticationConfigurations`-parametrarna för slutpunkten `/destinations`.
> 
>Läs [Konfiguration för kundautentisering](../functionality/destination-configuration/customer-authentication.md) om du vill ha mer information om vilka autentiseringstyper som stöds.

Använd den här API-slutpunkten om du bara vill skapa en autentiseringskonfiguration om det finns ett globalt autentiseringssystem mellan Adobe och målplattformen, och [!DNL Experience Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till målet. I det här fallet måste du skapa en autentiseringskonfiguration med API-slutpunkten `/credentials`.

När du använder ett globalt autentiseringssystem måste du ange `"authenticationRule":"PLATFORM_AUTHENTICATION"` i konfigurationen för [målleverans](../functionality/destination-configuration/destination-delivery.md) när du [skapar en ny målkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för autentiseringsuppgifter {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Hämta en konfiguration för autentiseringsuppgifter {#retrieve}

Du kan hämta en [befintlig](create-credential-configuration.md)-autentiseringskonfiguration genom att göra en `GET`-begäran till `/authoring/credentials`-slutpunkten.

**API-format**

Använd följande API-format för att hämta alla autentiseringskonfigurationer för ditt konto.

```http
GET /authoring/credentials
```

Använd följande API-format för att hämta en specifik autentiseringskonfiguration som definieras av parametern `{INSTANCE_ID}`.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Följande två begäranden hämtar alla autentiseringskonfigurationer för din IMS-organisation, eller en specifik autentiseringskonfiguration, beroende på om du skickar parametern `INSTANCE_ID` i begäran.

Välj varje flik nedan för att visa motsvarande nyttolast.

>[!BEGINTABS]

>[!TAB Hämta alla autentiseringskonfigurationer]

+++Begäran

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med en lista över autentiseringskonfigurationer som du har åtkomst till, baserat på det [!DNL IMS Org ID]- och sandlådenamn som du använde. En `instanceId` motsvarar en autentiseringskonfiguration.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Hämta en specifik autentiseringskonfiguration]

+++Begäran

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för den autentiseringskonfiguration som du vill hämta. |

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om autentiseringskonfigurationen som motsvarar `instanceId` som anges i begäran.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du hämtar information om dina autentiseringskonfigurationer med API-slutpunkten `/authoring/credentials`. Läs [hur du använder Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) och få en förståelse för var det här steget passar in i processen att konfigurera ditt mål.
