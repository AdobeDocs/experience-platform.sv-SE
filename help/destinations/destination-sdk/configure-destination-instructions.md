---
description: På den här sidan beskrivs hur du använder referensinformationen i konfigurationsalternativen för SDK för destinationer för att konfigurera destinationen med SDK för destinationer.
seo-description: This page describes how to use the reference information in Configuration options for the Destinations SDK to configure your destination using Destination SDK.
seo-title: How to use Destination SDK to configure your destination
title: Så här använder du mål-SDK för att konfigurera ditt mål
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: 15626393bd69173195dd924c8817073b75df5a1e
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Så här använder du mål-SDK för att konfigurera ditt mål

## Översikt {#overview}

På den här sidan beskrivs hur du använder referensinformationen i [Konfigurationsalternativ i Destinations SDK](./configuration-options.md) för att konfigurera målet. Stegen beskrivs i sekventiell ordning nedan.

## Förutsättningar {#prerequisites}

Innan du går vidare till stegen som visas nedan bör du läsa [sidan Komma igång för mål-SDK](./getting-started.md) för information om hur du får de autentiseringsuppgifter för Adobe I/O och andra krav som krävs för att arbeta med mål-SDK API:er.

## Steg för att använda konfigurationsalternativen i mål-SDK för att konfigurera destinationen {#steps}

![Illustrerade steg för att använda SDK-målslutpunkter](./assets/destination-sdk-steps.png)

## Steg 1: Skapa en server- och mallkonfiguration {#create-server-template-configuration}

Börja med att skapa en server- och mallkonfiguration med `/destinations-server`-slutpunkten (läs [API-referens](./destination-server-api.md)). Mer information om server- och mallkonfigurationen finns i [Server- och mallspecifikationerna](./configuration-options.md#server-and-template) i referensavsnittet.

Nedan visas ett exempel på en konfiguration. Observera att meddelandetransformeringsmallen i parametern `requestBody.value` hanteras i steg 3, [Skapa omformningsmall](./configure-destination-instructions.md#create-transformation-template).

```json
POST platform.adobe.io/data/core/activation/authoring/destination-servers

{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"insert after you create a template in step 3"
      },
      "contentType":"application/json"
   }
}
```

## Steg 2: Skapa målkonfiguration {#create-destination-configuration}

Nedan visas ett exempel på en konfiguration för en målmall som skapats med API-slutpunkten `/destinations`. Mer information om den här mallen finns i [Målkonfiguration](./destination-configuration.md).

Om du vill ansluta server- och mallkonfigurationen i steg 1 till den här målkonfigurationen lägger du till instans-ID:t för servern och mallkonfigurationen som `destinationServerId` här.

```json
POST platform.adobe.io/data/core/activation/authoring/destinations
 
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":""
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },   
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "aggregationPolicyId":null,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":null
         },
         "splitUserById":true,
         "maxBatchAgeInSecs":360,
         "maxNumEventsInBatch":100
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ]
}
```

## Steg 3: Skapa meddelandeomvandlingsmall - använd mallspråk för att ange meddelandets utdataformat {#create-transformation-template}

Beroende på vilka nyttolaster målet har stöd för måste du skapa en mall som omformar formatet för exporterade data från Adobe XDM-formatet till ett format som stöds av målet. Se mallexempel i avsnittet [Använda ett mallspråk för identitets-, attribut- och segmentmedlemsomvandlingar](./message-format.md#using-templating) och använd [mallutvecklingsverktyget](./create-template.md) som tillhandahålls av Adobe.

När du har skapat en meddelandeomformningsmall som fungerar för dig lägger du till den i server- och mallkonfigurationen som du skapade i steg 1.

## Steg 4: Skapa konfiguration för målgruppsmetadata {#create-audience-metadata-configuration}

För vissa destinationer kräver mål-SDK att du konfigurerar en målgruppsmetadatakonfiguration för att skapa, uppdatera eller ta bort målgrupper i ditt mål programmatiskt. Mer information om när du behöver konfigurera konfigurationen och hur du gör den finns i [Hantering av målgruppsmetadata](./audience-metadata-management.md).

Om du använder en konfiguration för målgruppsmetadata måste du ansluta den till målkonfigurationen som du skapade i steg 2. Lägg till instans-ID:t för målgruppens metadatakonfiguration i målkonfigurationen som `audienceTemplateId`.

## Steg 5: Skapa konfiguration av autentiseringsuppgifter/Konfigurera autentisering {#set-up-authentication}

Beroende på om du anger `"authenticationRule": "CUSTOMER_AUTHENTICATION"` eller `"authenticationRule": "PLATFORM_AUTHENTICATION"` i målkonfigurationen ovan, kan du ställa in autentisering för ditt mål med hjälp av slutpunkten `/destination` eller `/credentials`.

* **Mest vanliga fall**: Om du valde  `"authenticationRule": "CUSTOMER_AUTHENTICATION"` i målkonfigurationen och målet stöder autentiseringsmetoden OAuth 2 läser du  [OAuth 2-autentisering](./oauth2-authentication.md).
* Om du valde `"authenticationRule": "PLATFORM_AUTHENTICATION"`, se [Konfiguration av autentiseringsuppgifter](./credentials-configuration.md) i referensdokumentationen.

## Steg 6: Testa destinationen {#test-destination}

När du har konfigurerat ditt mål med hjälp av konfigurationsslutpunkterna i de föregående stegen kan du använda [måltestningsverktyget](./create-template.md) för att testa integrationen mellan Adobe Experience Platform och ditt mål.

Som en del av processen för att testa destinationen måste du använda användargränssnittet i Experience Platform för att skapa segment, som du aktiverar för destinationen. Se de två resurserna nedan för instruktioner om hur du skapar segment i Experience Platform:

* [Skapa en dokumentationssida för segment](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Skapa en segmentvideogenomgång](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)


## Steg 7: Publicera destinationen {#publish-destination}

När du har konfigurerat och testat målet kan du skicka konfigurationen till Adobe för granskning med API:t [målpublicering](./destination-publish-api.md).

## Steg 8: Dokumentera destinationen {#document-destination}

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktiserad integrering](./overview.md#productized-custom-integrations) använder du [självbetjäningsdokumentationsprocessen](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience League målkatalogen](/help/destinations/catalog/overview.md).
