---
description: Den här sidan innehåller exempel på det API-anrop som används för att ta bort en befintlig målserverkonfiguration via Adobe Experience Platform Destination SDK.
title: Ta bort en målserverkonfiguration
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# Ta bort en målserverkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en befintlig målserverkonfiguration med API-slutpunkten `/authoring/destination-servers`.

En detaljerad beskrivning av de funktioner som du kan ta bort via den här slutpunkten finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Mallspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Meddelandeformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Filformateringskonfiguration](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målserver {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Ta bort en målserverkonfiguration {#delete}

Du kan ta bort en [befintlig](create-destination-server.md) målserverkonfiguration genom att göra en `DELETE`-begäran till `/authoring/destination-servers`-slutpunkten med `{INSTANCE_ID}` för målserverkonfigurationen som du vill ta bort.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Om du vill hämta en befintlig målserverkonfiguration och dess motsvarande `{INSTANCE_ID}` kan du läsa artikeln om att [hämta en målserverkonfiguration](retrieve-destination-server.md).

**API-format**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` för målserverkonfigurationen som du vill ta bort. |

+++Begäran

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++svar

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du tar bort en befintlig målserver via API-slutpunkten för Destinationen SDK `/authoring/destination-servers`.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Skapa en målserverkonfiguration](create-destination-server.md)
* [Hämta en målserverkonfiguration](retrieve-destination-server.md)
* [Uppdatera en målserverkonfiguration](update-destination-server.md)
