---
description: På den här sidan visas ett exempel på API-anropet som används för att hämta en autentiseringskonfiguration via Adobe Experience Platform Destination SDK.
title: Hämta en konfiguration för autentiseringsuppgifter
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Hämta en konfiguration för autentiseringsuppgifter

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att hämta en autentiseringskonfiguration med `/authoring/credentials` API-slutpunkt.

## När ska du använda `/credentials` API-slutpunkt {#when-to-use}

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

Läs igenom [komma igång-guide](../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Hämta en konfiguration för autentiseringsuppgifter {#retrieve}

Du kan hämta en [befintlig](create-credential-configuration.md) konfiguration av autentiseringsuppgifter genom att göra en `GET` begäran till `/authoring/credentials` slutpunkt.

**API-format**

Använd följande API-format för att hämta alla autentiseringskonfigurationer för ditt konto.

```http
GET /authoring/credentials
```

Använd följande API-format för att hämta en specifik autentiseringskonfiguration, som definieras av `{INSTANCE_ID}` parameter.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Följande två förfrågningar hämtar alla autentiseringskonfigurationer för din IMS-organisation, eller en specifik autentiseringskonfiguration, beroende på om du skickar `INSTANCE_ID` -parametern i begäran.

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

Ett lyckat svar returnerar HTTP-status 200 med en lista över de autentiseringskonfigurationer som du har åtkomst till, baserat på [!DNL IMS Org ID] och namnet på sandlådan som du använde. Ett `instanceId` motsvarar en autentiseringskonfiguration.

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

Ett lyckat svar returnerar HTTP-status 200 med information om konfigurationen för autentiseringsuppgifter som motsvarar `instanceId` anges på begäran.

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

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du hämtar information om dina autentiseringskonfigurationer med `/authoring/credentials` API-slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
