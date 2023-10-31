---
description: På den här sidan visas ett exempel på API-anropet som används för att ta bort en Adobe Experience Platform Destination SDK för konfiguration av autentiseringsuppgifter.
title: Ta bort en autentiseringskonfiguration
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Ta bort en autentiseringskonfiguration

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en autentiseringskonfiguration med hjälp av `/authoring/credentials` API-slutpunkt.

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

## Ta bort en autentiseringskonfiguration {#delete}

Du kan ta bort en [befintlig](create-credential-configuration.md) konfiguration av autentiseringsuppgifter genom att göra en `DELETE` begäran till `/authoring/credentials` slutpunkt med `{INSTANCE_ID}`av den autentiseringskonfiguration som du vill ta bort.

Hämta en befintlig målkonfiguration och dess motsvarande `{INSTANCE_ID}`, se artikeln om [hämta en autentiseringskonfiguration](retrieve-credential-configuration.md).

**API-format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | The `ID` för den autentiseringskonfiguration du vill ta bort. |

Följande begäran tar bort en autentiseringskonfiguration som definierats av `{INSTANCE_ID}` parameter.

+++Begäran

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

+++

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du tar bort en autentiseringskonfiguration med `/authoring/credentials` API-slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
