---
description: Lär dig hur du strukturerar ett API-anrop för att skapa en målkonfiguration via Adobe Experience Platform Destination SDK.
title: Skapa en målkonfiguration
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Skapa en målkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en egen målkonfiguration med API-slutpunkten `/authoring/destinations`.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i följande artiklar:

* [Konfiguration av kundautentisering](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2-auktorisering](../../functionality/destination-configuration/oauth2-authorization.md)
* [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md)
* [Gränssnittsattribut](../../functionality/destination-configuration/ui-attributes.md)
* [Schemakonfiguration](../../functionality/destination-configuration/schema-configuration.md)
* [Konfiguration av namnutrymme för identitet](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Destinationsleverans](../../functionality/destination-configuration/destination-delivery.md)
* [Konfiguration av målgruppsmetadata](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Konfiguration av målgruppsmetadata](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Samlingsprincip](../../functionality/destination-configuration/aggregation-policy.md)
* [Batchkonfiguration](../../functionality/destination-configuration/batch-configuration.md)
* [Krav på historisk profil](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målkonfiguration {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa en målkonfiguration {#create}

Du kan skapa en ny målkonfiguration genom att göra en POST-begäran till slutpunkten `/authoring/destinations`.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API-format**

```http
POST /authoring/destinations
```

Följande begäran skapar en ny [!DNL Amazon S3]-destinationskonfiguration, konfigurerad med parametrarna som anges i nyttolasten. Nyttolasten nedan innehåller alla parametrar för filbaserade mål som accepteras av slutpunkten `/authoring/destinations`.

Observera att du inte behöver lägga till alla parametrar i API-anropet och att nyttolasten kan anpassas enligt dina API-krav.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Anger målets titel i Experience Platform-katalogen. |
| `description` | Sträng | Ange en beskrivning som Adobe ska använda i Experience Platform destinationskatalog för ditt destinationskort. Rikta dig för högst 4-5 meningar. ![Experience Platform-gränssnittsbild som visar målbeskrivningen.](../../assets/authoring-api/destination-configuration/destination-description.png "Målbeskrivning"){width="100" zoomable="yes"} |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED` och `DELETED`. Använd `TEST` när du först konfigurerar ditt mål. |
| `customerAuthenticationConfigurations.authType` | Sträng | Anger den konfiguration som används för att autentisera Experience Platform-kunder till målservern. Mer information om vilka autentiseringstyper som stöds finns i [konfiguration för kundautentisering](../../functionality/destination-configuration/customer-authentication.md). |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). ![Experience Platform-gränssnittsbild med kunddatafält.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Kunddatafält"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer`. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas av kunder i Experience Platform användargränssnitt. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `customerDataFields.default` | Sträng | Definierar standardvärdet från en `enum`-lista. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID till exempel inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i det här fältet. <br/><br/> Mer information om de här inställningarna finns i [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md). |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [målkatalogen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html#catalog) för ditt mål. Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på målet. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en`. Observera att den här länken fungerar först när Adobe har publicerat din destination och dokumentationen. <br/><br/> Mer information om de här inställningarna finns i [Gränssnittsattribut](../../functionality/destination-configuration/ui-attributes.md). ![Experience Platform-gränssnittsbild som visar dokumentationslänken.](../../assets/authoring-api/destination-configuration/documentation-url.png "Dokumentations-URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html#destination-categories). Använd ett av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Mer information om de här inställningarna finns i [Gränssnittsattribut](../../functionality/destination-configuration/ui-attributes.md). |
| `uiAttributes.connectionType` | Sträng | Vilken typ av anslutning det är, beroende på målet. Värden som stöds: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Sträng | Hänvisar till den typ av dataexport som stöds av målet. Ange `Streaming` för API-baserade integreringar eller `Batch` när du exporterar filer till dina mål. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om kunder kan mappa standardprofilattribut till identiteten som du konfigurerar. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan mappa identiteter som tillhör [anpassade namnutrymmen](/help/identity-service/features/namespaces.md#manage-namespaces) till identiteten som du konfigurerar. |
| `identityNamespaces.externalId.transformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när kunden [!DNL Experience Platform] har oformaterade e-postadresser som attribut och din plattform bara accepterar hashkodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Anger vilka [standardidentitetsnamnutrymmen](/help/identity-service/features/namespaces.md#standard) (till exempel IDFA) som kunder kan mappa till identiteten som du konfigurerar. <br> När du använder `acceptedGlobalNamespaces` kan du använda `"requiredTransformation":"sha256(lower($))"` för att skriva ned gemener och skicka e-postadresser eller telefonnummer med hash-kod. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Experience Platform]-kunder ansluter till ditt mål. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om Experience Platform-kunder loggar in på ditt system via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du kan till exempel välja det här alternativet om du även har markerat `authType: OAUTH2` eller `authType:BEARER` i `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och ditt mål och kunden [!DNL Experience Platform] inte behöver ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med hjälp av konfigurationen för [autentiseringsuppgifter-API](../../credentials-api/create-credential-configuration.md) och skicka autentiseringsuppgiftsobjektets ID i parametern `authenticationId` i konfigurationen för [målleverans](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication). </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | `instanceId` för [målservermallen](../destination-server/create-destination-server.md) som används för det här målet. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när målgrupper aktiveras till målet. Ange alltid detta till `true`. |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om målgruppsmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Kontrollerar om målgruppsmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform målgrupps-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Kontrollerar om målgruppsmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform målgruppsnamn. |
| `segmentMappingConfig.audienceTemplateId` | Sträng | `instanceId` för [målgruppens metadatamall](../../metadata-api/create-audience-template.md) som används för det här målet. |
| `schemaConfig.profileFields` | Array | När du lägger till fördefinierade `profileFields` enligt konfigurationen ovan kan användare välja att mappa Experience Platform-attribut till de fördefinierade attributen på målsidan. |
| `schemaConfig.profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `schemaConfig.segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Använd `true` om du vill att användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |

{style="table-layout:auto"}

+++

+++Svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målkonfigurationen.

+++

## API-felhantering

Destination SDK API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skapar en ny destinationskonfiguration via API-slutpunkten för Destination SDK `/authoring/destinations`.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Hämta en målkonfiguration](retrieve-destination-configuration.md)
* [Uppdatera en målkonfiguration](update-destination-configuration.md)
* [Ta bort en målkonfiguration](delete-destination-configuration.md)

Mer information om var den här slutpunkten passar in i målredigeringsprocessen finns i följande artiklar:

* [Använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
