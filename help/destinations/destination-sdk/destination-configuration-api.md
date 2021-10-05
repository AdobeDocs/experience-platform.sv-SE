---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/destination`.
title: Slutpunktsåtgärder för mål-API
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: c334a11ff6a03b38883a5319bc41cbe3f93c0289
workflow-type: tm+mt
source-wordcount: '2407'
ht-degree: 1%

---

# API-åtgärder för destinationsslutpunkt {#destination-configuration}

>[!IMPORTANT]
>
>**API-slutpunkt**:  `platform.adobe.io/data/core/activation/authoring/destinations`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/destinations`. En beskrivning av de funktioner som stöds av den här slutpunkten finns i [målkonfigurationen](./destination-configuration.md).

## Komma igång med mål-API-åtgärder {#get-started}

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa konfiguration för ett mål {#create}

Du kan skapa en ny målkonfiguration genom att göra en POST-förfrågan till `/authoring/destinations`-slutpunkten.

**API-format**


```http
POST /authoring/destinations
```

**Begäran**

Följande begäran skapar en ny destinationskonfiguration, konfigurerad med parametrarna i nyttolasten. Nyttolasten nedan innehåller alla parametrar som accepteras av slutpunkten `/authoring/destinations`. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
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
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Anger målets namn i Experience Platform-katalogen |
| `description` | Sträng | Ange en beskrivning som Adobe ska använda i Experience Platform-destinationskatalogen för ditt destinationskort. Rikta dig för högst 4-5 meningar. |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED` och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `customerAuthenticationConfigurations` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder mot servern. Se `authType` nedan för godkända värden. |
| `customerAuthenticationConfigurations.authType` | Sträng | Godkända värden är `OAUTH2, BEARER`. |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer` |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas av kunderna i användargränssnittet i Experience Platform |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID till exempel inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i det här fältet. |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [målkatalogen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog). Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på målet. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en`. |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Sträng | `Server-to-server` är för närvarande det enda tillgängliga alternativet. |
| `uiAttributes.frequency` | Sträng | `Streaming` är för närvarande det enda tillgängliga alternativet. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om målet accepterar standardprofilattribut. Normalt framhävs dessa attribut i våra partners dokumentation. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan ställa in anpassade namnutrymmen i målet. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när [!DNL Platform]-kunden har oformaterade e-postadresser som attribut och din plattform bara accepterar hash-kodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Används för fall där plattformen accepterar [standardnamnutrymmen för identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (till exempel IDFA), så du kan begränsa plattformsanvändare till att endast välja dessa ID-namnutrymmen. <br> När du använder  `acceptedGlobalNamespaces`kan du använda gemener  `"requiredTransformation":"sha256(lower($))"` och hash-adresser eller telefonnummer. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Platform]-kunder ansluter till ditt mål. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du skulle till exempel välja det här alternativet om du även valde `authType: OAUTH2` eller `authType:BEARER` i `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av konfigurationen [Credentials](./credentials-configuration.md). </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | `instanceId` för [målservermallen](./destination-server-api.md) som används för det här målet. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`:  [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`:  [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | `instanceId` för [målgruppens metadatamall](./audience-metadata-api.md) som används för det här målet. |
| `schemaConfig.profileFields` | Array | När du lägger till fördefinierade `profileFields` som visas i konfigurationen ovan, kan användare välja att mappa Experience Platform-attribut till de fördefinierade attributen på målsidan. |
| `schemaConfig.profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `schemaConfig.segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Använd `true` om du vill att användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |
| `aggregation.aggregationType` | – | Välj antingen `BEST_EFFORT` eller `CONFIGURABLE_AGGREGATION`. I exempelkonfigurationen ovan ingår `BEST_EFFORT`-aggregering. Ett exempel på `CONFIGURABLE_AGGREGATION` finns i exempelkonfigurationen i dokumentet [målkonfiguration](./destination-configuration.md#example-configuration). Observera att de parametrar som är relevanta för konfigurerbar aggregering beskrivs nedan i denna tabell. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Heltal | Experience Platform kan samla flera exporterade profiler i ett enda HTTP-anrop. Ange maximalt antal profiler som din slutpunkt ska ta emot i ett enda HTTP-anrop. Observera att detta är en bästa ansträngningsaggregering. Om du till exempel anger värdet 100 kan Platform skicka valfritt antal profiler som är mindre än 100 på ett samtal. <br> Om servern inte accepterar flera användare per begäran anger du värdet 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolean | Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop för ett givet namnområde. |
| `aggregation.configurableAggregation.splitUserById` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop för ett givet namnområde. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Heltal | *Högsta värde: 3600*. Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Tillsammans med `maxNumEventsInBatch` avgör detta hur länge Experience Platform ska vänta tills ett API-anrop skickas till slutpunkten. <br> Om du till exempel använder maxvärdet för båda parametrarna väntar Experience Platform antingen 3600 sekunder ELLER tills det finns 10 000 kvalificerade profiler innan API-anropet görs, beroende på vilket som inträffar först. |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Heltal | *Högsta värde: 10000*. Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Se `maxBatchAgeInSecs` ovan. |
| `aggregation.configurableAggregation.aggregationKey` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Gör att du kan sammanställa de exporterade profilerna som är mappade till målet baserat på parametrarna nedan: <br> <ul><li>segment-ID</li><li> segmentstatus </li><li> identity namespace </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Ange `true` om du vill gruppera profiler som exporterats till ditt mål efter segment-ID. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Du måste ange både `includeSegmentId:true` och `includeSegmentStatus:true` om du vill gruppera profiler som exporterats till ditt mål efter segment-ID OCH segmentstatus. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Ange `true` om du vill gruppera profiler som exporterats till ditt mål efter identitetsnamnområde. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Använd den här parametern för att ange om du vill att de exporterade profilerna ska samlas i grupper av en enda identitet (GAID, IDFA, telefonnummer, e-post osv.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Sträng | Se parametern i exempelkonfigurationen [här](./destination-configuration.md#example-configuration). Skapa listor med identitetsgrupper om du vill gruppera profiler som exporterats till ditt mål av grupper med identitetsnamnutrymme. Du kan t.ex. kombinera profiler som innehåller IDFA- och GAID-mobilidentifierare i ett samtal till din destination och e-postmeddelanden i ett annat genom att använda konfigurationen i exemplet. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målkonfigurationen.

## Visa målkonfigurationer {#retrieve-list}

Du kan hämta en lista över alla målkonfigurationer för din IMS-organisation genom att göra en GET-begäran till `/authoring/destinations`-slutpunkten.

**API-format**


```http
GET /authoring/destinations
```

**Begäran**

Följande begäran hämtar listan över målkonfigurationer som du har åtkomst till, baserat på IMS-organisationens och sandlådekonfigurationer.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Följande svar returnerar HTTP-status 200 med en lista över målkonfigurationer som du har åtkomst till, baserat på IMS-organisationens ID och det sandlådenamn som du använde. Ett `instanceId` motsvarar mallen för ett mål. Svaret kortas av för att vara kortfattat.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
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
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Anger målets namn i Experience Platform-katalogen. |
| `description` | Sträng | Ange en beskrivning som Adobe ska använda i Experience Platform-destinationskatalogen för ditt destinationskort. Rikta dig för högst 4-5 meningar. |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED` och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `customerAuthenticationConfigurations` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder mot servern. Se `authType` nedan för godkända värden. |
| `customerAuthenticationConfigurations.authType` | Sträng | Godkända värden är `OAUTH2, BEARER`. |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer` |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas av kunderna i användargränssnittet i Experience Platform |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID till exempel inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i det här fältet. |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [målkatalogen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog). Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på målet. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en` |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Sträng | `Server-to-server` är för närvarande det enda tillgängliga alternativet. |
| `uiAttributes.frequency` | Sträng | `Streaming` är för närvarande det enda tillgängliga alternativet. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om målet accepterar standardprofilattribut. Normalt framhävs dessa attribut i våra partners dokumentation. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan ställa in anpassade namnutrymmen i målet. Läs mer om [anpassade namnutrymmen](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) i Adobe Experience Platform. |
| `identityNamespaces.externalId.allowedAttributesTransformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när [!DNL Platform]-kunden har oformaterade e-postadresser som attribut och din plattform bara accepterar hash-kodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Används för fall där plattformen accepterar [standardnamnutrymmen för identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (till exempel IDFA), så du kan begränsa plattformsanvändare till att endast välja dessa ID-namnutrymmen. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Platform]-kunder ansluter till ditt mål. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du skulle till exempel välja det här alternativet om du även valde `authType: OAUTH2` eller `authType:BEARER` i `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och [!DNL Platform]-kunden inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av konfigurationen [Credentials](./credentials-configuration.md). </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | `instanceId` för [målservermallen](./destination-server-api.md) som används för det här målet. |
| `destConfigId` | Sträng | Det här fältet genereras automatiskt och kräver inte dina indata. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`:  [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`:  [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | `instanceId` för [målgruppens metadatamall](./audience-metadata-management.md) som används för det här målet. Läs [API-referensen för målgruppsmetadata](./audience-metadata-api.md) om du vill konfigurera en metadatamall för målgrupper. |

{style=&quot;table-layout:auto&quot;}

## Uppdatera en befintlig målkonfiguration {#update}

Du kan uppdatera en befintlig målkonfiguration genom att göra en PUT-begäran till `/authoring/destinations`-slutpunkten och ange instans-ID:t för den målkonfiguration som du vill uppdatera. Ange den uppdaterade målkonfigurationen i anropets brödtext.

**API-format**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målkonfigurationen som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar en befintlig destinationskonfiguration som konfigurerats med parametrarna i nyttolasten. I exempelanropet nedan uppdaterar vi konfigurationen [som skapades tidigare](./destination-configuration-api.md#create) för att nu acceptera GAID, IDFA och hash-kodade e-postidentifierare som identitetsnamnutrymmen.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Hämta en specifik målkonfiguration {#get}

Du kan hämta detaljerad information om en viss målkonfiguration genom att göra en GET-begäran till `/authoring/destinations`-slutpunkten och ange instans-ID:t för den målkonfiguration som du vill hämta.

**API-format**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målkonfigurationen som du vill hämta. |

**Begäran**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna målkonfigurationen.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Ta bort en specifik målkonfiguration {#delete}

Du kan ta bort den angivna målkonfigurationen genom att göra en DELETE-begäran till `/authoring/destinations`-slutpunkten och ange ID:t för målkonfigurationen som du vill ta bort i sökvägen till begäran.

**API-format**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | `id` för målkonfigurationen som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering

SDK API-målslutpunkterna följer de allmänna felmeddelandeprinciperna för Experience Platform-API. Se [API-statuskoder](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) och [begäranrubrikfel](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du konfigurerar målet med API-slutpunkten `/authoring/destinations`. Läs [hur du använder mål-SDK för att konfigurera ditt mål](./configure-destination-instructions.md) och förstå var det här steget passar in i processen att konfigurera ditt mål.
