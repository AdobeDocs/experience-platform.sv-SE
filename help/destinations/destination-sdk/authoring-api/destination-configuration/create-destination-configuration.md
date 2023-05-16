---
description: Lär dig strukturera ett API-anrop för att skapa en målkonfiguration via Adobe Experience Platform Destination SDK.
title: Skapa en målkonfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# Skapa en målkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en egen målkonfiguration med hjälp av `/authoring/destinations` API-slutpunkt.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i följande artiklar:

* [Konfiguration av kundautentisering](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2-autentisering](../../functionality/destination-configuration/oauth2-authentication.md)
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
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målkonfiguration {#get-started}

Läs igenom [komma igång-guide](../../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa en målkonfiguration {#create}

Du kan skapa en ny destinationskonfiguration genom att göra en POST-förfrågan till `/authoring/destinations` slutpunkt.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API-format**

```http
POST /authoring/destinations
```

Följande begäran skapar en ny [!DNL Amazon S3] destinationskonfiguration, konfigurerad med parametrarna i nyttolasten. Nyttolasten nedan innehåller alla parametrar för filbaserade destinationer som accepteras av `/authoring/destinations` slutpunkt.

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
| `name` | Sträng | Anger målets namn i Experience Platform-katalogen. |
| `description` | Sträng | Ange en beskrivning som Adobe ska använda i Experience Platform-destinationskatalogen för ditt destinationskort. Rikta dig för högst 4-5 meningar. ![Plattformsgränssnittsbild som visar målbeskrivningen.](../../assets/authoring-api/destination-configuration/destination-description.png "Målbeskrivning"){width="100" zoomable="yes"} |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED`och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `customerAuthenticationConfigurations.authType` | Sträng | Anger konfigurationen som används för att autentisera Experience Platform-kunder till målservern. Se [konfiguration för kundautentisering](../../functionality/destination-configuration/customer-authentication.md) för detaljerad information om vilka autentiseringstyper som stöds. |
| `customerDataFields.name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. ![Plattformsgränssnittsbild som visar kunddatafält.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Kunddatafält"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer`. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `customerDataFields.title` | Sträng | Anger fältets namn, så som det visas för kunder i användargränssnittet i Experience Platform. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `customerDataFields.description` | Sträng | Ange en beskrivning för det anpassade fältet. Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `customerDataFields.isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `customerDataFields.enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `customerDataFields.default` | Sträng | Definierar standardvärdet från ett `enum` lista. |
| `customerDataFields.pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID:n inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i detta fält. <br/><br/> Se [Kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) för detaljerad information om dessa inställningar. |
| `uiAttributes.documentationLink` | Sträng | Refererar till dokumentationssidan i [Målkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) till destinationen. Använd `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på destinationen. För ett mål som heter Moviestar använder du `https://www.adobe.com/go/destinations-moviestar-en`. Observera att den här länken bara fungerar när Adobe har aktiverat målet och dokumentationen har publicerats. <br/><br/> Se [Gränssnittsattribut](../../functionality/destination-configuration/ui-attributes.md) för detaljerad information om dessa inställningar. ![En bild av användargränssnittet för plattformen som visar dokumentationslänken.](../../assets/authoring-api/destination-configuration/documentation-url.png "Dokumentations-URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Se [Gränssnittsattribut](../../functionality/destination-configuration/ui-attributes.md) för detaljerad information om dessa inställningar. |
| `uiAttributes.connectionType` | Sträng | Vilken typ av anslutning det är, beroende på målet. Värden som stöds: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Sträng | Hänvisar till den typ av dataexport som stöds av målet. Ange till `Streaming` för API-baserade integreringar, eller `Batch` när du exporterar filer till dina mål. |
| `identityNamespaces.externalId.acceptsAttributes` | Boolean | Anger om kunder kan mappa standardprofilattribut till identiteten som du konfigurerar. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Boolean | Anger om kunderna kan mappa identiteter som tillhör [anpassade namnutrymmen](/help/identity-service/namespaces.md#manage-namespaces) till identiteten som du konfigurerar. |
| `identityNamespaces.externalId.transformation` | Sträng | _Visas inte i exempelkonfigurationen_. Används till exempel när [!DNL Platform] kunden har oformaterade e-postadresser som attribut och din plattform accepterar bara hashkodade e-postmeddelanden. Här anger du den omformning som ska användas (till exempel transformera e-postmeddelandet till gemener och sedan hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | – | Anger vilken [standardidentitetsnamnutrymmen](/help/identity-service/namespaces.md#standard) (till exempel IDFA)-kunder kan mappa till identiteten som du konfigurerar. <br> När du använder `acceptedGlobalNamespaces`kan du använda `"requiredTransformation":"sha256(lower($))"` till gemener och hash-adresser eller telefonnummer. |
| `destinationDelivery.authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in på ditt system via ett användarnamn och lösenord, en innehavartoken eller någon annan autentiseringsmetod. Du kan t.ex. markera det här alternativet om du också har markerat `authType: OAUTH2` eller `authType:BEARER` in `customerAuthenticationConfigurations`. </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [API för autentiseringsuppgifter](../../credentials-api/create-credential-configuration.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationDelivery.destinationServerId` | Sträng | The `instanceId` i [målservermall](../destination-server/create-destination-server.md) används för detta mål. |
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. Ställ alltid in detta på `true`. |
| `segmentMappingConfig.mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `segmentMappingConfig.audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](../../metadata-api/create-audience-template.md) används för detta mål. |
| `schemaConfig.profileFields` | Array | När du lägger till fördefinierade `profileFields` som visas i konfigurationen ovan, kan användare mappa Experience Platform-attribut till de fördefinierade attributen på målsidan. |
| `schemaConfig.profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `schemaConfig.segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Boolean | Använd `true` om du vill att användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målkonfigurationen.

+++

## API-felhantering

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du skapar en ny målkonfiguration via Destinationen SDK `/authoring/destinations` API-slutpunkt.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Hämta en målkonfiguration](retrieve-destination-configuration.md)
* [Uppdatera en målkonfiguration](update-destination-configuration.md)
* [Ta bort en målkonfiguration](delete-destination-configuration.md)

Mer information om var den här slutpunkten passar in i målredigeringsprocessen finns i följande artiklar:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
