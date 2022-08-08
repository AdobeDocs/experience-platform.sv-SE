---
description: På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med API-slutpunkten `/authoring/destination`.
title: Slutpunktsåtgärder för mål-API
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '2572'
ht-degree: 1%

---

# API-åtgärder för destinationsslutpunkt {#destination-configuration}

>[!IMPORTANT]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

På den här sidan visas och beskrivs alla API-åtgärder som du kan utföra med `/authoring/destinations` API-slutpunkt. En beskrivning av de funktioner som stöds av den här slutpunkten finns i [målkonfiguration](./destination-configuration.md).

## Komma igång med mål-API-åtgärder {#get-started}

Läs igenom [komma igång-guide](./getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa konfiguration för ett direktuppspelningsmål {#create}

Du kan skapa en ny destinationskonfiguration genom att göra en POST-förfrågan till `/authoring/destinations` slutpunkt.

**API-format**

```http
POST /authoring/destinations
```

**Begäran**

Följande begäran skapar en ny konfiguration för direktuppspelningsmålet, konfigurerad med parametrarna som anges i nyttolasten. Nedan finns alla parametrar för direktuppspelningsdestinationer som accepteras av `/authoring/destinations` slutpunkt. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED`och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `customerAuthenticationConfigurations` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder mot servern. Se `authType` nedan för godkända värden. |
| `customerAuthenticationConfigurations.authType` | Sträng | Värden som stöds för direktuppspelningsmål är: <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> Värden som stöds för filbaserade mål är: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer` |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas av kunderna i användargränssnittet i Experience Platform |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID:n inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i detta fält. |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [Målkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) till destinationen. Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på destinationen. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en`. Observera att den här länken bara fungerar när Adobe har aktiverat målet och dokumentationen har publicerats. |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Sträng | `Server-to-server` är för närvarande det enda tillgängliga alternativet. |
| `uiAttributes.frequency` | Sträng | `Streaming` är för närvarande det enda tillgängliga alternativet. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om målet accepterar standardprofilattribut. Normalt framhävs dessa attribut i våra partners dokumentation. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan ställa in anpassade namnutrymmen i målet. |
| `identityNamespaces.externalId.transformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när [!DNL Platform] kunden har oformaterade e-postadresser som attribut och din plattform accepterar bara hashkodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Används för fall där plattformen godkänner [standardidentitetsnamnutrymmen](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (till exempel IDFA), så du kan begränsa Platform-användare till att endast välja dessa identitetsnamnutrymmen. <br> När du använder `acceptedGlobalNamespaces`kan du använda `"requiredTransformation":"sha256(lower($))"` till gemener och hash-adresser eller telefonnummer. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in på ditt system via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du kan t.ex. markera det här alternativet om du också har markerat `authType: OAUTH2` eller `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [Autentiseringsuppgifter](./credentials-configuration-api.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | The `instanceId` i [målservermall](./destination-server-api.md) används för detta mål. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`: [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`: [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](./audience-metadata-api.md) används för detta mål. |
| `schemaConfig.profileFields` | Array | När du lägger till fördefinierade `profileFields` som visas i konfigurationen ovan, kan användare mappa Experience Platform-attribut till de fördefinierade attributen på målsidan. |
| `schemaConfig.profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `schemaConfig.segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Använd `true` om du vill att användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |
| `aggregation.aggregationType` | – | Välj antingen `BEST_EFFORT` eller `CONFIGURABLE_AGGREGATION`. I exempelkonfigurationen ovan ingår `BEST_EFFORT` aggregering. Ett exempel på `CONFIGURABLE_AGGREGATION`, se exempelkonfigurationen i [målkonfiguration](./destination-configuration.md#example-configuration) -dokument. De parametrar som är relevanta för konfigurerbar aggregering beskrivs nedan i denna tabell. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Heltal | Experience Platform kan samla flera exporterade profiler i ett enda HTTP-anrop. Ange maximalt antal profiler som din slutpunkt ska ta emot i ett enda HTTP-anrop. Observera att detta är en bästa ansträngningsaggregering. Om du till exempel anger värdet 100 kan Platform skicka valfritt antal profiler som är mindre än 100 på ett samtal. <br> Om servern inte accepterar flera användare per begäran anger du värdet 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Boolean | Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop, för ett givet namnutrymme. |
| `aggregation.configurableAggregation.splitUserById` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Använd den här flaggan om anropet till målet ska delas efter identitet. Ange den här flaggan som `true` om servern bara accepterar en identitet per anrop, för ett givet namnutrymme. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Heltal | <ul><li>*Minsta värde: 1800*</li><li>*Högsta värde: 3600*</li><li>Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Konfigurera ett värde mellan lägsta och högsta godkända värden. Tillsammans med `maxNumEventsInBatch`anger den här parametern hur länge Experience Platform ska vänta tills ett API-anrop skickas till slutpunkten. <br> Om du till exempel använder maxvärdet för båda parametrarna, väntar Experience Platform antingen 3 600 sekunder ELLER tills det finns 10 000 kvalificerade profiler innan API-anropet görs, beroende på vilket som inträffar först. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Heltal | <ul><li>*Minsta värde: 1000*</li><li>*Högsta värde: 10000*</li><li>Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Konfigurera ett värde mellan lägsta och högsta godkända värden. En beskrivning av den här parametern finns på `maxBatchAgeInSecs` precis ovanför.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Gör att du kan sammanställa de exporterade profilerna som är mappade till målet baserat på parametrarna nedan: <br> <ul><li>segment-ID</li><li> segmentstatus </li><li> identity namespace </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Ange detta till `true` om du vill gruppera profiler som exporterats till ditt mål efter segment-ID. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Du måste ange båda `includeSegmentId:true` och `includeSegmentStatus:true` om du vill gruppera profiler som exporterats till ditt mål efter segment-ID OCH segmentstatus. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Ange detta till `true` om du vill gruppera profiler som exporterats till ditt mål efter identitetsnamnutrymme. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Boolean | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Använd den här parametern för att ange om du vill att de exporterade profilerna ska samlas i grupper av en enda identitet (GAID, IDFA, telefonnummer, e-post osv.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Sträng | Se parameter i exempelkonfiguration [här](./destination-configuration.md#example-configuration). Skapa listor med identitetsgrupper om du vill gruppera profiler som exporterats till ditt mål av grupper med identitetsnamnutrymme. Du kan t.ex. kombinera profiler som innehåller IDFA- och GAID-mobilidentifierare i ett samtal till din destination och e-postmeddelanden i ett annat genom att använda konfigurationen i exemplet. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målkonfigurationen.

## Skapa konfiguration för ett filbaserat mål {#create-file-based}

Du kan skapa en ny destinationskonfiguration genom att göra en POST-förfrågan till `/authoring/destinations` slutpunkt.

**API-format**

```http
POST /authoring/destinations
```

**Begäran**

Följande begäran skapar en ny [!DNL Amazon S3] filbaserad målkonfiguration, konfigurerad med parametrarna i nyttolasten. Nyttolasten nedan innehåller alla parametrar för filbaserade destinationer som accepteras av `/authoring/destinations` slutpunkt. Observera att du inte behöver lägga till alla parametrar i anropet och att mallen kan anpassas enligt dina API-krav.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
            "allowedExportMode":[
                "DAILY_FULL_EXPORT",
                "FIRST_FULL_THEN_INCREMENTAL"
            ],
            "allowedScheduleFrequency":[
                "DAILY",
                "EVERY_3_HOURS",
                "EVERY_6_HOURS",
                "EVERY_8_HOURS",
                "EVERY_12_HOURS",
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Detaljerade beskrivningar av alla parametrar ovan finns i [filbaserad målkonfiguration](file-based-destination-configuration.md).

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målkonfigurationen.

## Visa målkonfigurationer {#retrieve-list}

Du kan hämta en lista över alla destinationskonfigurationer för din IMS-organisation genom att göra en GET-förfrågan till `/authoring/destinations` slutpunkt.

**API-format**


```http
GET /authoring/destinations
```

**Begäran**

Följande begäran hämtar listan över målkonfigurationer som du har åtkomst till, baserat på IMS-organisationens och sandlådekonfigurationer.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED`och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `customerAuthenticationConfigurations` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder mot servern. Se `authType` nedan för godkända värden. |
| `customerAuthenticationConfigurations.authType` | Sträng | Godkända värden är `OAUTH2, BEARER`. |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer` |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas av kunderna i användargränssnittet i Experience Platform |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID:n inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i detta fält. |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [Målkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) till destinationen. Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på destinationen. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en`. Observera att den här länken bara fungerar när Adobe har aktiverat målet och dokumentationen har publicerats. |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Sträng | `Server-to-server` är för närvarande det enda tillgängliga alternativet. |
| `uiAttributes.frequency` | Sträng | `Streaming` är för närvarande det enda tillgängliga alternativet. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om målet accepterar standardprofilattribut. Normalt framhävs dessa attribut i våra partners dokumentation. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan ställa in anpassade namnutrymmen i målet. Läs mer om [anpassade namnutrymmen](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) i Adobe Experience Platform. |
| `identityNamespaces.externalId.transformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när [!DNL Platform] kunden har oformaterade e-postadresser som attribut och din plattform accepterar bara hashkodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Används för fall där plattformen godkänner [standardidentitetsnamnutrymmen](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (till exempel IDFA), så du kan begränsa Platform-användare till att endast välja dessa identitetsnamnutrymmen. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in på ditt system via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du kan t.ex. markera det här alternativet om du också har markerat `authType: OAUTH2` eller `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [Autentiseringsuppgifter](./authentication-configuration.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | The `instanceId` i [målservermall](./destination-server-api.md) används för detta mål. |
| `destConfigId` | Sträng | Det här fältet genereras automatiskt och kräver inte dina indata. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`: [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`: [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](./audience-metadata-management.md) används för detta mål. Om du vill konfigurera en metadatamall för målgrupper läser du [API-referens för målgruppsmetadata](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Uppdatera en befintlig målkonfiguration {#update}

Du kan uppdatera en befintlig destinationskonfiguration genom att göra en PUT-begäran till `/authoring/destinations` slutpunkt och ange instans-ID för målkonfigurationen som du vill uppdatera. Ange den uppdaterade målkonfigurationen i anropets brödtext.

**API-format**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målkonfigurationen som du vill uppdatera. |

**Begäran**

Följande begäran uppdaterar en befintlig destinationskonfiguration som konfigurerats med parametrarna i nyttolasten. I exempelsamtalet nedan uppdaterar vi konfigurationen [skapades tidigare](./destination-configuration-api.md#create) att nu godkänna GAID, IDFA och hash-kodade e-postidentifierare som identitetsnamnutrymmen.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Du kan hämta detaljerad information om en viss destinationskonfiguration genom att göra en GET-förfrågan till `/authoring/destinations` slutpunkt och ange instans-ID för målkonfigurationen som du vill hämta.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Du kan ta bort den angivna målkonfigurationen genom att göra en DELETE-begäran till `/authoring/destinations` slutpunkt och ange ID:t för målkonfigurationen som du vill ta bort i sökvägen för begäran.

**API-format**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{INSTANCE_ID}` | The `id` för den målkonfiguration som du vill ta bort. |

**Begäran**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 tillsammans med ett tomt HTTP-svar.

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du konfigurerar ditt mål med `/authoring/destinations` API-slutpunkt. Läs [Så här använder du Destination SDK för att konfigurera ditt mål](./configure-destination-instructions.md) för att förstå var det här steget passar in i processen att konfigurera målet.
