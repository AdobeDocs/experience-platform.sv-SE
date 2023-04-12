---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/Destations/publish`.
title: API-slutpunktsåtgärder för publiceringsmål
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# API-åtgärder för publiceringsdestinationsslutpunkt {#publish-destination}

>[!IMPORTANT]
>
>Du behöver bara använda den här API-slutpunkten om du skickar en produkterad (offentlig) destination som ska användas av andra Experience Platform-kunder. Om du skapar ett privat mål för eget bruk behöver du inte skicka målet formellt med publicerings-API:t.

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med `/authoring/destinations/publish` API-slutpunkt.

När du har konfigurerat och testat destinationen kan du skicka den till Adobe för granskning och publicering. Läs [Skicka för granskning av ett mål som skapats i Destination SDK](./submit-destination.md) för alla andra steg som du måste göra som en del av målöverföringsprocessen.

Använd API-slutpunkten för publiceringsmål för att skicka en publiceringsbegäran när:

* Som Destination SDK partner vill ni att alla kunder i Experience Platform ska kunna använda er av den producerade destinationen,
* Du skapar *alla uppdateringar* till dina konfigurationer. Konfigurationsuppdateringar visas endast i målet när du har skickat in en ny publiceringsbegäran som har godkänts av Experience Platform-teamet.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

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
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du skickar för publicering. Hämta mål-ID:t för en målkonfiguration med [API-referens för destinationskonfiguration](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Sträng | Använd `ALL` för att din destination ska visas i katalogen för alla Experience Platform-kunder. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar HTTP-status 201 med information om din målpubliceringsbegäran.

## Lista målpubliceringsbegäranden {#retrieve-list}

Du kan hämta en lista över alla mål som skickats in för publicering för din organisation genom att göra en GET-förfrågan till `/authoring/destinations/publish` slutpunkt.

**API-format**

```http
GET /authoring/destinations/publish
```

**Begäran**

Följande begäran hämtar listan över mål som skickats in för publicering som du har tillgång till, baserat på organisation och sandlådekonfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över mål som skickats in för publicering som du har tillgång till, baserat på det organisations-ID och sandlådans namn som du använde. Ett `configId` motsvarar publiceringsbegäran för ett mål.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du har skickat in för publicering. |
| `publishDetailsList.configId` | Sträng | Det unika ID:t för målpubliceringsbegäran för det skickade målet. |
| `publishDetailsList.allowedOrgs` | Sträng | Returnerar de Experience Platform-organisationer som målet är tillgängligt för. <br> <ul><li> För `"destinationType": "PUBLIC"`returneras `"*"`, vilket innebär att destinationen är tillgänglig för alla Experience Platform-organisationer.</li><li> För `"destinationType": "DEV"`returnerar den här parametern organisations-ID:t för organisationen som du använde för att redigera och testa målet.</li></ul> |
| `publishDetailsList.status` | Sträng | Status för målpubliceringsbegäran. Möjliga värden är `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinationer med värdet `PUBLISHED` är direktsända och kan användas av Experience Platform-kunder. |
| `publishDetailsList.destinationType` | Sträng | Typ av mål. Värden kan vara `DEV` och `PUBLIC`. `DEV` motsvarar destinationen i din Experience Platform-organisation. `PUBLIC` motsvarar målet som du har skickat in för publicering. Tänk på de här två alternativen i Git-termer, där `DEV` versionen representerar din lokala redigeringsgren och `PUBLIC` version representerar fjärrhuvudgrenen. |
| `publishDetailsList.publishedDate` | Sträng | Det datum då målet skickades för publicering, i epoktid. |

{style="table-layout:auto"}

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skickar en publiceringsbegäran för ditt mål. Adobe Experience Platform-teamet granskar din publiceringsförfrågan och kommer tillbaka till dig inom fem arbetsdagar.
