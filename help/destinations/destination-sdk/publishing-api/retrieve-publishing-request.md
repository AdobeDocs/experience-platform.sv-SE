---
description: Den här sidan innehåller exempel på API-anropet som används för att hämta information om en destinationspubliceringsbegäran via Adobe Experience Platform Destination SDK.
title: Hämta en publiceringsbegäran för mål
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Hämta en publiceringsbegäran för mål

>[!IMPORTANT]
>
>Du behöver bara använda den här API-slutpunkten om du skickar en produkterad (offentlig) destination som ska användas av andra Experience Platform-kunder. Om du skapar ett privat mål för eget bruk behöver du inte skicka målet formellt med publicerings-API:t.

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

När du har konfigurerat och testat destinationen kan du skicka den till Adobe för granskning och publicering. Läs [Skicka för granskning av ett mål som har skapats i Destination SDK](../guides/submit-destination.md) för alla andra steg som du måste göra som en del av målöverföringsprocessen.

Använd API-slutpunkten för publiceringsmål för att skicka en publiceringsbegäran när:

* Som Destination SDK partner vill ni att alla kunder i Experience Platform ska kunna använda er av den producerade destinationen,
* Du gör *alla uppdateringar* till dina konfigurationer. Konfigurationsuppdateringar visas endast i målet när du har skickat in en ny publiceringsbegäran som har godkänts av Experience Platform-teamet.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målpublicering {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Lista målpubliceringsbegäranden {#retrieve-list}

Du kan hämta en lista över alla mål som skickats in för publicering för din IMS-organisation genom att göra en GET-förfrågan till slutpunkten `/authoring/destinations/publish`.

**API-format**

Använd följande API-format för att hämta alla publiceringsbegäranden för ditt konto.

```http
GET /authoring/destinations/publish
```

Använd följande API-format för att hämta en specifik publiceringsbegäran, som definieras av parametern `{DESTINATION_ID}`.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Begäran**

Följande två begäranden hämtar alla publiceringsbegäranden för din IMS-organisation, eller en specifik publiceringsbegäran, beroende på om du skickar parametern `DESTINATION_ID` i begäran.

Välj varje flik nedan för att visa motsvarande nyttolast.

>[!BEGINTABS]

>[!TAB Hämta alla publiceringsbegäranden]

+++Begäran

Följande begäran hämtar listan över publiceringsbegäranden som du har skickat, baserat på [!DNL IMS Org ID]- och sandlådekonfigurationen.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++svar

Följande svar returnerar HTTP-status 200 med en lista över alla mål som skickats in för publicering som du har tillgång till, baserat på IMS-organisations-ID:t och namnet på den sandlåda som du använde. Ett `configId` motsvarar publiceringsbegäran för ett mål.

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

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `destinationId` | Sträng | Mål-ID för målkonfigurationen som du har skickat in för publicering. |
| `publishDetailsList.configId` | Sträng | Det unika ID:t för målpubliceringsbegäran för det skickade målet. |
| `publishDetailsList.allowedOrgs` | Sträng | Returnerar de Experience Platform-organisationer som målet är tillgängligt för. <br> <ul><li> För `"destinationType": "PUBLIC"` returnerar den här parametern `"*"`, vilket innebär att målet är tillgängligt för alla organisationer i Experience Platform.</li><li> För `"destinationType": "DEV"` returnerar den här parametern organisations-ID för den organisation som du använde för att redigera och testa målet.</li></ul> |
| `publishDetailsList.status` | Sträng | Status för målpubliceringsbegäran. Möjliga värden är `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinationer med värdet `PUBLISHED` är live och kan användas av Experience Platform-kunder. |
| `publishDetailsList.destinationType` | Sträng | Typ av mål. Värdena kan vara `DEV` och `PUBLIC`. `DEV` motsvarar målet i din Experience Platform-organisation. `PUBLIC` motsvarar målet som du har skickat in för publicering. Tänk på de här två alternativen i Git-termer, där versionen `DEV` representerar din lokala redigeringsgren och versionen `PUBLIC` representerar fjärrhuvudgrenen. |
| `publishDetailsList.publishedDate` | Sträng | Det datum då målet skickades för publicering, i epoktid. |

{style="table-layout:auto"}

+++

>[!TAB Hämta en specifik publiceringsbegäran]

+++Begäran

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{DESTINATION_ID}` | ID:t för destinationen som du vill hämta publiceringsstatusen för. |

+++

+++svar

Om du skickade `DESTINATION_ID` i API-anropet returnerar svaret HTTP-status 200 med detaljerad information om den angivna målpubliceringsbegäran.

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
| `publishDetailsList.allowedOrgs` | Sträng | Returnerar de Experience Platform-organisationer som målet är tillgängligt för. <br> <ul><li> För `"destinationType": "PUBLIC"` returnerar den här parametern `"*"`, vilket innebär att målet är tillgängligt för alla organisationer i Experience Platform.</li><li> För `"destinationType": "DEV"` returnerar den här parametern organisations-ID för den organisation som du använde för att redigera och testa målet.</li></ul> |
| `publishDetailsList.status` | Sträng | Status för målpubliceringsbegäran. Möjliga värden är `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinationer med värdet `PUBLISHED` är live och kan användas av Experience Platform-kunder. |
| `publishDetailsList.destinationType` | Sträng | Typ av mål. Värdena kan vara `DEV` och `PUBLIC`. `DEV` motsvarar målet i din Experience Platform-organisation. `PUBLIC` motsvarar målet som du har skickat in för publicering. Tänk på de här två alternativen i Git-termer, där versionen `DEV` representerar din lokala redigeringsgren och versionen `PUBLIC` representerar fjärrhuvudgrenen. |
| `publishDetailsList.publishedDate` | Sträng | Det datum då målet skickades för publicering, i epoktid. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.
