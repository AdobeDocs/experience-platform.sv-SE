---
description: Den här sidan innehåller exempel på det API-anrop som används för att ta bort en befintlig målgruppsmall via Adobe Experience Platform Destination SDK.
title: Ta bort en målgruppsmall
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# Ta bort en målgruppsmall

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att ta bort en målgruppsmall med hjälp av `/authoring/audience-templates` API-slutpunkt.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i [hantering av målgruppsmetadata](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målgruppsmallar {#get-started}

Läs igenom [komma igång-guide](../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Ta bort en målgruppsmall {#delete}

Du kan ta bort en [befintlig](create-audience-template.md) målgruppsmall genom att skapa `DELETE` begäran till `/authoring/audience-templates` slutpunkt med `{INSTANCE_ID}`av målgruppsmallen som du vill ta bort.

Så här hämtar du en befintlig målgruppsmall och dess motsvarande `{INSTANCE_ID}`, se artikeln om [hämta en målgruppsmall](retrieve-audience-template.md).

**API-format**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | The `ID` för målgruppsmallen som du vill ta bort. |

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

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du tar bort en målgruppsmall med `/authoring/audience-templates` API-slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](../guides/configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
