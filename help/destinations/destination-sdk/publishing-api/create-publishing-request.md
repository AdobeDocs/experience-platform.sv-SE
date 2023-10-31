---
description: Lär dig hur du formaterar ett API-anrop för att skicka en begäran om målpublicering via Adobe Experience Platform Destination SDK.
title: Skapa en publiceringsbegäran för destinationen
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Skapa en publiceringsbegäran för destinationen

>[!IMPORTANT]
>
>Du behöver bara använda den här API-slutpunkten om du skickar en produkterad (offentlig) destination som ska användas av andra Experience Platform-kunder. Om du skapar ett privat mål för eget bruk behöver du inte skicka målet formellt med publicerings-API:t.

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

När du har konfigurerat och testat destinationen kan du skicka den till Adobe för granskning och publicering. Läs [Skicka för granskning av ett mål som skapats i Destination SDK](../guides/submit-destination.md) för alla andra steg som du måste göra som en del av målinlämningsprocessen.

Använd API-slutpunkten för publiceringsmål för att skicka en publiceringsbegäran när:

* Som Destination SDK partner vill ni att alla kunder i Experience Platform ska kunna använda er av den producerade destinationen,
* Du skapar *alla uppdateringar* till dina konfigurationer. Konfigurationsuppdateringar visas endast i målet när du har skickat in en ny publiceringsbegäran som har godkänts av Experience Platform-teamet.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målpublicering {#get-started}

Innan du fortsätter bör du granska [komma igång-guide](../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skicka en målkonfiguration för publicering {#create}

Du kan skicka en målkonfiguration för publicering genom att göra en POST-förfrågan till `/authoring/destinations/publish` slutpunkt.

**API-format**

```http
POST /authoring/destinations/publish
```

+++Begäran

Följande begäran skickar en publiceringsdestination i de organisationer som konfigurerats med parametrarna i nyttolasten. Nedan finns alla parametrar som accepteras av `/authoring/destinations/publish` slutpunkt.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du skickar för publicering. Hämta mål-ID:t för en målkonfiguration med [hämta en destinationskonfiguration](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API-anrop. |
| `destinationAccess` | Sträng | Använd `ALL` för att din destination ska visas i katalogen för alla Experience Platform-kunder. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 201 med information om din målpubliceringsbegäran.

+++

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skickar en publiceringsbegäran för ditt mål. Adobe Experience Platform-teamet granskar din publiceringsförfrågan och kommer tillbaka till dig inom fem arbetsdagar.
