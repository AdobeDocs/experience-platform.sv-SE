---
description: På den här sidan visas ett exempel på API-anropet som används för att ta bort en autentiseringskonfiguration i Adobe Experience Platform Destination SDK.
title: Ta bort en autentiseringskonfiguration
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Ta bort en autentiseringskonfiguration

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`.

## När API-slutpunkten `/credentials` ska användas {#when-to-use}

>[!IMPORTANT]
>
>I de flesta fall behöver du ***inte*** använda API-slutpunkten `/credentials`. I stället kan du konfigurera autentiseringsinformationen för målet via `customerAuthenticationConfigurations`-parametrarna för slutpunkten `/destinations`.
> 
>Läs [Konfiguration för kundautentisering](../functionality/destination-configuration/customer-authentication.md) om du vill ha mer information om vilka autentiseringstyper som stöds.

Använd den här API-slutpunkten om du bara vill skapa en autentiseringskonfiguration om det finns ett globalt autentiseringssystem mellan Adobe och målplattformen, och [!DNL Experience Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till målet. I det här fallet måste du skapa en autentiseringskonfiguration med API-slutpunkten `/credentials`.

När du använder ett globalt autentiseringssystem måste du ange `"authenticationRule":"PLATFORM_AUTHENTICATION"` i konfigurationen för [målleverans](../functionality/destination-configuration/destination-delivery.md) när du [skapar en ny målkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md). Sedan måste du skapa en [autentiseringskonfiguration](../credentials-api/create-credential-configuration.md) och skicka ID:t för autentiseringsuppgiftsobjektet i parametern `authenticationId` i konfigurationen för [målleverans](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för autentiseringsuppgifter {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Ta bort en autentiseringskonfiguration {#delete}

Du kan ta bort en [befintlig](create-credential-configuration.md)-autentiseringskonfiguration genom att göra en `DELETE`-begäran till `/authoring/credentials`-slutpunkten med `{INSTANCE_ID}` för den autentiseringskonfiguration som du vill ta bort.

Om du vill hämta en befintlig destinationskonfiguration och dess motsvarande `{INSTANCE_ID}` kan du läsa artikeln om att [hämta en autentiseringskonfiguration](retrieve-credential-configuration.md).

**API-format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` för den autentiseringskonfiguration som du vill ta bort. |

Följande begäran tar bort en autentiseringskonfiguration som definieras av parametern `{INSTANCE_ID}`.

+++Begäran

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Svar

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

+++

## API-felhantering {#error-handling}

Destination SDK API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg {#next-steps}

När du har läst det här dokumentet kan du nu ta bort en autentiseringskonfiguration med API-slutpunkten `/authoring/credentials`. Läs [hur du använder Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) och få en förståelse för var det här steget passar in i processen att konfigurera ditt mål.
