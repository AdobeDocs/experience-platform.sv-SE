---
description: Den här sidan innehåller exempel på det API-anrop som används för att ta bort en befintlig målkonfiguration via Adobe Experience Platform Destination SDK.
title: Ta bort en målkonfiguration
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Ta bort en målkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en befintlig målkonfiguration med API-slutpunkten `/authoring/destinations`.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målkonfiguration {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Ta bort en målkonfiguration {#delete}

Du kan ta bort en [befintlig](create-destination-configuration.md) målserverkonfiguration genom att göra en `DELETE`-begäran till `/authoring/destinations`-slutpunkten med `{INSTANCE_ID}` för målkonfigurationen som du vill ta bort.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Om du vill hämta en befintlig målkonfiguration och dess motsvarande `{INSTANCE_ID}` läser du artikeln om [att hämta en målkonfiguration](retrieve-destination-configuration.md).

**API-format**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` för målkonfigurationen som du vill ta bort. |

+++Begäran

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++svar

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.


## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du tar bort en befintlig målkonfiguration via API-slutpunkten för Destinationen SDK `/authoring/destinations`.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Skapa en målkonfiguration](create-destination-configuration.md)
* [Hämta en målkonfiguration](retrieve-destination-configuration.md)
* [Uppdatera en målkonfiguration](update-destination-configuration.md)
