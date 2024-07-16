---
description: Den här sidan innehåller exempel på det API-anrop som används för att ta bort en befintlig målgruppsmall via Adobe Experience Platform Destination SDK.
title: Ta bort en målgruppsmall
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Ta bort en målgruppsmall

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en målgruppsmall med API-slutpunkten `/authoring/audience-templates`.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i [hantering av målgruppsmetadata](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målgruppsmallar {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Ta bort en målgruppsmall {#delete}

Du kan ta bort en [befintlig](create-audience-template.md) målgruppsmall genom att göra en `DELETE`-förfrågan till `/authoring/audience-templates`-slutpunkten med `{INSTANCE_ID}` för målgruppsmallen som du vill ta bort.

Om du vill hämta en befintlig målgruppsmall och dess motsvarande `{INSTANCE_ID}` kan du läsa artikeln om att [hämta en målgruppsmall](retrieve-audience-template.md).

**API-format**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` för målgruppsmallen som du vill ta bort. |

+++Begäran

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
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

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du tar bort en målgruppsmall med API-slutpunkten `/authoring/audience-templates`. Läs [om hur du använder Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
