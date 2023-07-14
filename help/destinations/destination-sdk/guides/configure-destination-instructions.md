---
description: På den här sidan visas och beskrivs stegen för hur du konfigurerar ett mål för direktuppspelning med Destination SDK.
title: Använd Destination SDK för att konfigurera ett direktuppspelningsmål
exl-id: d8aa7353-ba55-4a0d-81c4-ea2762387638
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Använd Destination SDK för att konfigurera ett direktuppspelningsmål

## Översikt {#overview}

Den här sidan beskriver hur du använder informationen i [Konfigurationsalternativ i mål-SDK](../functionality/configuration-options.md) och i andra Destinationer SDK och API-referensdokument för att konfigurera [direktuppspelningsmål](../../destination-types.md#streaming-destinations). Stegen beskrivs i sekventiell ordning nedan.

## Förutsättningar {#prerequisites}

Innan du går vidare till stegen som visas nedan ska du läsa [Komma igång med Destination SDK](../getting-started.md) för information om hur du får de autentiseringsuppgifter för Adobe I/O och andra krav som krävs för att arbeta med Destination SDK-API:er. Detta förutsätter att du har slutfört villkoren för partnerskap och behörighet och är redo att börja utveckla ditt mål.

## Steg för att använda konfigurationsalternativen i Destinationen SDK för att konfigurera destinationen {#steps}

![Illustrerade steg för att använda Destinationens SDK slutpunkter](../assets/guides/destination-sdk-steps.png)

## Steg 1: Skapa en server- och mallkonfiguration {#create-server-template-configuration}

Starta med [skapa en server- och mallkonfiguration](../authoring-api/destination-server/create-destination-server.md) med `/destinations-server` slutpunkt.

Nedan visas ett exempel på en konfiguration. Observera att mallen för meddelandeomformning i `requestBody.value` parametern behandlas i steg 3, [Skapa omformningsmall](#create-transformation-template).

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json {line-numbers="true" highlight="14"}
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

Nedan visas ett exempel på en konfiguration för en målmall som skapats med `/destinations` API-slutpunkt. Se [skapa en målkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md) för mer information.

Om du vill ansluta server- och mallkonfigurationen i steg 1 till den här målkonfigurationen lägger du till instans-ID:t för servern och mallkonfigurationen som `destinationServerId` här.

>[!IMPORTANT]
>
>Om du vill skapa ett korrekt konfigurerat mål för realtid (direktuppspelning) *måste* lägg till minst en målidentitet i `identityNamespaces`, vilket visas nedan. Om ingen målidentitet har konfigurerats kan användarna inte fortsätta förbi [Mappningssteg](../../ui/activate-segment-streaming-destinations.md#mapping) aktiveringsarbetsflödet.

```shell
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="74"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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

Beroende på vilka nyttolaster målet har stöd för måste du skapa en mall som omformar formatet för exporterade data från Adobe XDM-formatet till ett format som stöds av målet. Se mallexempel i avsnittet [Använda ett mallspråk för omvandlingar av identitet, attribut och målgruppsmedlemskap](../functionality/destination-server/message-format.md#using-templating) och använder [mallutvecklingsverktyg](../testing-api/streaming-destinations/create-template.md) tillhandahålls av Adobe.

När du har skapat en meddelandeomformningsmall som fungerar för dig lägger du till den i server- och mallkonfigurationen som du skapade i steg 1.

```json {line-numbers="true" highlight="13-14"}
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
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"users\": [\n        {% for profile in input.profiles %}\n            {{profile|raw}}{% if not loop.last %},{% endif %}\n        {% endfor %}\n    ]\n}"
      },
      "contentType":"application/json"
   }
}
```

## Steg 4: Skapa konfiguration för målgruppsmetadata {#create-audience-metadata-configuration}

För vissa destinationer kräver Destinationen SDK att du konfigurerar en målgruppsmetadatakonfiguration för att skapa, uppdatera eller ta bort målgrupper i målgruppen. Se [Hantering av målgruppsmetadata](../functionality/audience-metadata-management.md) om du vill ha information om när du behöver konfigurera den här konfigurationen och hur du gör det.

Om du använder en konfiguration för målgruppsmetadata måste du ansluta den till målkonfigurationen som du skapade i steg 2. Lägg till instans-ID:t för målgruppens metadatakonfiguration i målkonfigurationen som `audienceTemplateId`.

```json {line-numbers="true" highlight="53"}
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
   "audienceMetadataConfig":{
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
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000
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


## Steg 5: Konfigurera autentisering {#set-up-authentication}

Beroende på om du anger `"authenticationRule": "CUSTOMER_AUTHENTICATION"` eller `"authenticationRule": "PLATFORM_AUTHENTICATION"` i målkonfigurationen ovan kan du konfigurera autentisering för målet med hjälp av `/destination` eller `/credentials` slutpunkt.

Om du valde `"authenticationRule": "CUSTOMER_AUTHENTICATION"` i målkonfigurationen och målet stöder autentiseringsmetoden OAuth 2, läs [OAuth 2-autentisering](../functionality/destination-configuration/oauth2-authentication.md).

Om du valde `"authenticationRule": "PLATFORM_AUTHENTICATION"`måste du skapa en [konfiguration av autentiseringsuppgifter](../credentials-api/create-credential-configuration.md).

## Steg 6: Testa destinationen {#test-destination}

När du har konfigurerat målet med hjälp av konfigurationsslutpunkterna i föregående steg kan du använda kommandot [måltestningsverktyg](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) för att testa integrationen mellan Adobe Experience Platform och ditt mål.

Som en del av processen för att testa destinationen måste du använda användargränssnittet i Experience Platform för att skapa segment, som du aktiverar för destinationen. Se de två resurserna nedan för instruktioner om hur du skapar målgrupper i Experience Platform:

* [Skapa en publikdokumentationssida](/help/segmentation/ui/overview.md#create-segment)
* [Skapa en videopresentation](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Steg 7: Publicera destinationen {#publish-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

När du har konfigurerat och testat destinationen använder du [målpublicerings-API](../publishing-api/create-publishing-request.md) för att skicka in din konfiguration till Adobe för granskning.

## Steg 8: Dokumentera destinationen {#document-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktionsintegrering](../overview.md#productized-custom-integrations), använder du [självbetjäningsdokumentationsprocess](../docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience Platform destinationskatalog](/help/destinations/catalog/overview.md).

## Steg 9: Skicka mål för Adobe granskning {#submit-for-review}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Innan destinationen kan publiceras i Experience Platform-katalogen och vara synlig för alla Experience Platform-kunder måste du skicka in destinationen för Adobe granskning officiellt. Hitta fullständig information om hur [skicka för granskning en produkterad destination som skapats i Destination SDK](../guides/submit-destination.md).
