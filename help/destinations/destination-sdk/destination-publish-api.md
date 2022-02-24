---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/Destations/publish`.
title: API-slutpunktsåtgärder för publiceringsmål
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 6ad556e3b7bf15f1d6ff522307ff232b8fd947d3
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 2%

---

# API-åtgärder för publiceringsdestinationsslutpunkt {#publish-destination}

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med `/authoring/destinations/publish` API-slutpunkt.

När du har konfigurerat och testat destinationen kan du skicka den till Adobe för granskning och publicering.

Använd API-slutpunkten för publiceringsmål för att skicka en publiceringsbegäran när:

* Som Destination SDK partner vill ni att alla kunder i Experience Platform ska kunna använda er av den producerade destinationen,
* Du vill göra ditt anpassade mål tillgängligt i din egen Experience Platform-organisation, i alla sandlådor.

## Komma igång med API-åtgärder för målpublicering {#get-started}

Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skicka en målkonfiguration för publicering {#create}

Du kan skicka en målkonfiguration för publicering genom att göra en POST-förfrågan till `/authoring/destinations/publish` slutpunkt.

**API-format**

```http
POST /authoring/destinations/publish
```

**Begäran**

Följande begäran skickar en publiceringsdestination i de organisationer som konfigurerats med parametrarna i nyttolasten. Nedan finns alla parametrar som accepteras av `/authoring/destinations/publish` slutpunkt.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du skickar för publicering. Hämta mål-ID:t för en målkonfiguration med [API-referens för destinationskonfiguration](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Sträng | `ALL` eller `LIMITED`. Ange om du vill att destinationen ska visas i katalogen för alla Experience Platform-kunder eller bara för vissa organisationer. <br> **Anteckning**: Om du använder `LIMITED`publiceras målet endast för din Experience Platform-organisation. Om du vill publicera destinationen till en delgrupp av Experience Platform-organisationer för kundtestning kan du kontakta supporten för Adobe. |
| `allowedOrgs` | Sträng | Om du använder `"destinationAccess":"LIMITED"`, ange för vilka Experience Platform-organisationer destinationen ska vara tillgänglig. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om din målpubliceringsbegäran.

## Lista målpubliceringsbegäranden {#retrieve-list}

Du kan hämta en lista över alla mål som skickats in för publicering för din IMS-organisation genom att göra en GET-förfrågan till `/authoring/destinations/publish` slutpunkt.

**API-format**

```http
GET /authoring/destinations/publish
```

**Begäran**

Följande begäran hämtar listan över mål som skickats in för publicering som du har tillgång till, baserat på IMS-organisationens och sandlådekonfigurationens.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över mål som skickats in för publicering som du har tillgång till, baserat på IMS-organisations-ID:t och det sandlådenamn som du använde. Ett `configId` motsvarar publiceringsbegäran för ett mål.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du har skickat in för publicering. |
| `publishDetailsList.configId` | Sträng | Det unika ID:t för målpubliceringsbegäran för det skickade målet. |
| `publishDetailsList.allowedOrgs` | Sträng | Returnerar de Experience Platform-organisationer som målet ska vara tillgängligt för. |
| `publishDetailsList.status` | Sträng | Status för målpubliceringsbegäran. Möjliga värden är `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | Sträng | Det datum då målet skickades för publicering, i epoktid. |

{style=&quot;table-layout:auto&quot;}

## Uppdatera en befintlig målpubliceringsbegäran {#update}

Du kan uppdatera de tillåtna organisationerna i en befintlig målpubliceringsbegäran genom att göra en PUT-begäran till `/authoring/destinations/publish` slutpunkt och ange ID för destinationen som du vill uppdatera de tillåtna organisationerna för. Ange de uppdaterade tillåtna organisationerna i samtalet.

**API-format**

```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för destinationen som du vill uppdatera publiceringsbegäran för. |

**Begäran**

Följande begäran uppdaterar en befintlig målpubliceringsbegäran som konfigurerats med parametrarna i nyttolasten. I exempelsamtalet nedan uppdaterar vi de tillåtna organisationerna.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## Hämta status för en specifik målpubliceringsbegäran {#get}

Du kan hämta detaljerad information om en viss målpubliceringsbegäran genom att göra en GET-förfrågan till `/authoring/destinations/publish` slutpunkt och ange ID för destinationen som du vill hämta publiceringsstatusen för.

**API-format**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för destinationen som du vill hämta publiceringsstatusen för. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna målpubliceringsbegäran.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skickar en publiceringsbegäran för ditt mål. Adobe Experience Platform-teamet granskar din publiceringsförfrågan och kommer tillbaka till dig inom fem arbetsdagar.
