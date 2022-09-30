---
description: Med den här konfigurationen kan du ange viktig information för ditt filbaserade mål, som målnamn, kategori, beskrivning och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål.
title: Filbaserade alternativ för destinationskonfiguration för Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: b32450311469ecf2af2ca45b3fa1feaf25147ea2
workflow-type: tm+mt
source-wordcount: '2985'
ht-degree: 2%

---

# Filbaserad målkonfiguration {#destination-configuration}

## Översikt {#overview}

Med den här konfigurationen kan du ange viktig information för ditt filbaserade mål, som målnamn, kategori, beskrivning och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål. Du kan också använda den här konfigurationen för att visa alternativ som är relaterade till filtypen, filformatet eller komprimeringsinställningarna för de exporterade filerna.

Den här konfigurationen kopplar även de andra konfigurationer som krävs för att målet ska fungera - målserver och målgruppsmetadata - till den här konfigurationen. Läs om hur du kan referera till de två konfigurationerna i en [avsnitt längre nedan](./file-based-destination-configuration.md#connecting-all-configurations).

Du kan konfigurera funktionerna som beskrivs i det här dokumentet med hjälp av `/authoring/destinations` API-slutpunkt. Läs [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Exempel på destinationskonfiguration för Amazon S3 {#batch-example-configuration}

Nedan visas ett exempel på en privat anpassad Amazon S3-destination som skapats via `/destinations` konfigurationsslutpunkt.

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
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
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
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
            "name":"phoneNo",
            "title":"phoneNo",
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
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Anger målets namn i Experience Platform-katalogen. |
| `description` | Sträng | Ange en beskrivning för destinationskortet i Experience Platform-katalogen. Rikta dig för högst 4-5 meningar. |
| `status` | Sträng | Anger målkortets livscykelstatus. Godkända värden är `TEST`, `PUBLISHED`och `DELETED`. Använd `TEST` när du först konfigurerar målet. |
| `maxProfileAttributes` | Sträng | Anger det maximala antalet profilattribut som kunder kan exportera till målet. Standardvärdet är `2000`. |
| `maxIdentityAttributes` | Sträng | Anger det maximala antalet ID-namnutrymmen som kunder kan exportera till målet. Standardvärdet är `10`. |

{style=&quot;table-layout:auto&quot;}

## Konfigurationer för kundautentisering {#customer-authentication-configurations}

Det här avsnittet i destinationskonfigurationen genererar [Konfigurera nytt mål](/help/destinations/ui/connect-destination.md) i användargränssnittet i Experience Platform, där användare ansluter Experience Platform till konton som de har med ditt mål.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Beroende på vilket [autentiseringsalternativ](authentication-configuration.md##supported-authentication-types) du anger i dialogrutan `authType` -fältet, genereras Experience Platform-sidan för användarna enligt följande:

### Amazon S3-autentisering {#s3}

När du konfigurerar autentiseringstypen för Amazon S3 måste användare ange autentiseringsuppgifterna för S3.

![Gränssnittsåtergivning med S3-autentisering](assets/s3-authentication-ui.png)

### Azure Blob-autentisering  {#blob}

När du konfigurerar autentiseringstypen Azure Blob måste användarna ange anslutningssträngen.

![Gränssnittsåtergivning med blobautentisering](assets/blob-authentication-ui.png)

### SFTP med lösenordsautentisering

När du konfigurerar SFTP med lösenordsautentiseringstypen måste användarna ange SFTP-användarnamn och -lösenord samt SFTP-domän och -port (standardport är 22).

![Gränssnittsrendering med SFTP med lösenordsautentisering](assets/sftp-password-authentication-ui.png)

### SFTP med autentisering med SSH-nyckel

När du konfigurerar SFTP med autentiseringstypen SSH-nyckel måste användarna ange SFTP-användarnamnet och SSH-nyckeln samt SFTP-domänen och -porten (standardporten är 22).

![Gränssnittsåtergivning med SFTP med SSH-nyckelautentisering](assets/sftp-key-authentication-ui.png)

## Kunddatafält {#customer-data-fields}

Använd det här avsnittet för att be användare fylla i anpassade fält, som är specifika för ditt mål, när de ansluter till målet i användargränssnittet i Experience Platform.

I exemplet nedan `customerDataFields` kräver att användare anger ett namn för sitt mål och anger [!DNL Amazon S3] filnamn och mappsökväg, liksom komprimeringstyp, filformat och flera andra filformateringsalternativ.

Du kan komma åt och använda kundindata från kunddatafält i mallar. Använd makrot `{{customerData.exampleName}}`. Om du till exempel ber användare att ange ett Amazon S3-bucket-fält, med namnet `bucket`kan du använda makrot till att få åtkomst till den i mallar `{{customerData.bucket}}`. Visa ett exempel på hur ett kunddatafält används i [målserverkonfiguration](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
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
```

>[!TIP]
>
>Alla filformateringskonfigurationer som listas i exemplet ovan beskrivs utförligt i [filformatskonfiguration](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) -avsnitt.

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `name` | Sträng | Ange ett namn för det anpassade fält som du introducerar. |
| `title` | Sträng | Anger fältets namn, så som det visas för kunder i användargränssnittet i Experience Platform. |
| `description` | Sträng | Ange en beskrivning för det anpassade fältet. |
| `type` | Sträng | Anger vilken typ av anpassat fält du introducerar. Godkända värden är `string`, `object`, `integer`. |
| `isRequired` | Boolean | Anger om det här fältet är obligatoriskt i arbetsflödet för målkonfiguration. |
| `pattern` | Sträng | Tvingar fram ett mönster för det anpassade fältet, om det behövs. Använd reguljära uttryck för att framtvinga ett mönster. Om dina kund-ID:n inte innehåller siffror eller understreck anger du `^[A-Za-z]+$` i detta fält. |
| `enum` | Sträng | Återger det anpassade fältet som en listruta och visar de alternativ som är tillgängliga för användaren. |
| `default` | Sträng | Definierar standardvärdet från ett `enum` lista. |

{style=&quot;table-layout:auto&quot;}

## Gränssnittsattribut {#ui-attributes}

Det här avsnittet hänvisar till de gränssnittselement i konfigurationen ovan som Adobe ska använda för ditt mål i Adobe Experience Platform användargränssnitt.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `documentationLink` | Sträng | Refererar till dokumentationssidan i [Målkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) till destinationen. Använd `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på destinationen. För ett mål som heter Moviestar använder du `http://www.adobe.com/go/destinations-moviestar-en`. Observera att den här länken bara fungerar när Adobe har aktiverat målet och dokumentationen har publicerats. |
| `category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Sträng | Den URL där du var värd för ikonen som ska visas på målkatalogkortet. För privata anpassade integreringar krävs inte detta. För producerade konfigurationer måste du dela en ikon med Adobe-teamet när du [skicka målet för granskning](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | Sträng | Vilken typ av anslutning det är, beroende på målet. Värden som stöds: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Boolean | Anger om målanslutningen ingår i [flödeskörningsgränssnitt](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). När inställningen är `true`: <ul><li>The **[!UICONTROL Last dataflow run date]** och **[!UICONTROL Last dataflow run status]** visas i målbläddringssidan.</li><li>The **[!UICONTROL Dataflow runs]** och **[!UICONTROL Activation data]** -flikar visas på målvysidan.</li></ul> |
| `monitoringSupported` | Boolean | Anger om målanslutningen ingår i [övervakningsgränssnitt](../ui/destinations-workspace.md#browse). När inställningen är `true`, **[!UICONTROL View in monitoring]** -alternativet visas på målbläddringssidan. |
| `frequency` | Sträng | Hänvisar till den typ av dataexport som stöds av målet. Ange till `Batch` för filbaserade mål. |

{style=&quot;table-layout:auto&quot;}

## Destinationsleverans {#destination-delivery}

Avsnittet om destinationsleverans anger exakt vart exporterade data ska skickas och vilken autentiseringsregel som används på den plats där data ska landas. Du måste ange en eller flera `destinationServerId`är var data levereras och autentiseringsregeln. I de flesta fall är autentiseringsregeln som du bör använda `CUSTOMER_AUTHENTICATION`.

The `deliveryMatchers` -avsnittet är valfritt och kan användas om du anger flera `destinationServerId`s. Om så är fallet, `deliveryMatchers` anger hur exporterade data ska delas mellan olika målservrar.

```json
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
   ]
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet på något av följande sätt: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [Autentiseringsuppgifter](./credentials-configuration-api.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `destinationServerId` | Sträng | The `instanceId` i [målserverkonfiguration](./server-and-file-configuration.md) som du [skapad](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) för detta mål. |

{style=&quot;table-layout:auto&quot;}

## Konfiguration av segmentmappning {#segment-mapping}

Det här avsnittet av målkonfigurationen gäller hur segmentmetadata, som segmentnamn eller ID:n, ska delas mellan Experience Platform och målet.

Via `audienceTemplateId`är det här avsnittet också kopplat den här konfigurationen till [konfiguration av målets metadata](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform-segmentnamnet. |
| `mapExperiencePlatformSegmentId` | Boolean | Anger om segmentmappnings-ID:t i målaktiveringsarbetsflödet är Experience Platform segment-ID:t. |
| `mapUserInput` | Boolean | Kontrollerar om segmentmappnings-ID:t i målaktiveringsarbetsflödet anges av användaren. |
| `audienceTemplateId` | Boolean | The `instanceId` i [metadatamall för målgrupper](./audience-metadata-management.md) används för detta mål. Om du vill konfigurera en metadatamall för målgrupper läser du [API-referens för målgruppsmetadata](./audience-metadata-api.md). |

## Schemakonfiguration i mappningssteget {#schema-configuration}

Adobe Experience Platform Destination SDK stöder partnerdefinierade scheman. Med ett partnerdefinierat schema kan användare mappa profilattribut och identiteter till anpassade scheman som definierats av målpartners, ungefär som med [mål för direktuppspelning](destination-configuration.md#schema-configuration) arbetsflöde.

Använd parametrarna i `schemaConfig` för att aktivera mappningssteget i arbetsflödet för målaktivering. Genom att använda de parametrar som beskrivs nedan kan du bestämma om användare av Experience Platform kan mappa profilattribut och/eller identiteter till ditt filbaserade mål.

Du kan skapa statiska, hårdkodade schemafält eller ange ett dynamiskt schema som Experience Platform ska ansluta till för att dynamiskt hämta och fylla i fält i mappningsarbetsflödets målschema. Målschemat visas på skärmbilden nedan.

![Skärmbild som markerar målschemafälten i mappningssteget i aktiveringsarbetsflödet.](/help/destinations/destination-sdk/assets/target-schema-fields.png)

### Konfiguration av statiskt hårdkodat schemafält

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `profileFields` | Array | När du lägger till fördefinierade `profileFields`kan Experience Platform-användare mappa plattformsattribut till de fördefinierade attributen i målet. |
| `profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `identityRequired` | Boolean | Använd `true` om användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |

{style=&quot;table-layout:auto&quot;}

### Dynamisk schemakonfiguration i mappningssteget {#dynamic-schema-configuration}

Använd parametrarna i  `dynamicSchemaConfig` för att dynamiskt hämta ditt eget schema som plattformsprofilattribut och/eller identiteter kan mappas till.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"2aa8a809-c4ae-4f66-bb02-12df2e0a2279",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `identityRequired` | Boolean | Använd `true` om användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |
| `destinationServerId` | Sträng | The `instanceId` i [målserverkonfiguration](./destination-server-api.md) som du skapade för ditt dynamiska schema. Den här målservern innehåller HTTP-slutpunkten som Experience Platform ska anropa för att hämta det dynamiska schema som används för att fylla i målfält. |
| `authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet på något av följande sätt: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [Autentiseringsuppgifter](./credentials-configuration-api.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `value` | Sträng | Namnet på det schema som ska visas i användargränssnittet i Experience Platform i mappningssteget. |
| `responseFormat` | Sträng | Alltid inställt på `SCHEMA` när du definierar ett anpassat schema. |

{style=&quot;table-layout:auto&quot;}

### Nödvändiga mappningar {#required-mappings}

I schemakonfigurationen kan du lägga till obligatoriska (eller fördefinierade) mappningar. Det här är mappningar som användare kan visa men inte ändra när de konfigurerar en anslutning till ditt mål. Du kan till exempel använda e-postadressfältet så att det alltid skickas till målet i de exporterade filerna. Nedan visas ett exempel på en schemakonfiguration med obligatoriska mappningar och hur den ser ut i mappningssteget i [aktivera data till batchmålarbetsflöde](/help/destinations/ui/activate-batch-profile-destinations.md).

```json
    "requiredMappingsOnly": true, // this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID", //if only the destination field is specified, then the user is able to select a source field to map to the destination.
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      },
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address" //when both source and destination fields are specified as required mappings, then the user can not select or edit any of the two fields and can only view the selection.
      },
      {
        "sourceType": "text/x.aep-xl",
        "source": "iif(${segmentMembership.ups.seg_id.status}==\"exited\", \"1\",\"0\")",
        "destination": "delete"
      }
    ] 
```

![Bild av mappningarna som krävs i UI-aktiveringsflödet.](/help/destinations/destination-sdk/assets/required-mappings.png)

>[!NOTE]
>
>Följande kombinationer av obligatoriska mappningar stöds för närvarande:
>* Du kan konfigurera ett obligatoriskt källfält och ett obligatoriskt målfält. I det här fallet kan användare inte redigera eller markera något av de två fälten och bara visa markeringen.
>* Du kan bara konfigurera ett obligatoriskt målfält. I det här fallet kan användarna välja ett källfält som ska kopplas till målet.
>
> Konfigurering av endast ett obligatoriskt källfält pågår *not* stöds.

Använd de parametrar som beskrivs i tabellen nedan om du vill lägga till obligatoriska mappningar i aktiveringsarbetsflödet för ditt mål.

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `requiredMappingsOnly` | Boolean | Anger om användare kan mappa andra attribut och identiteter i aktiveringsflödet, *skild från* de mappningar som du anger. |
| `requiredMappings.mandatoryRequired` | Boolean | Ange som true om det här fältet måste vara ett obligatoriskt attribut som alltid ska finnas i filexporten till ditt mål. Läs mer om [obligatoriska attribut](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | Boolean | Ange som true om det här fältet måste användas som en dedupliceringsnyckel vid filexport till ditt mål. Läs mer om [dedupliceringsnycklar](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | Sträng | Används när du konfigurerar ett källfält efter behov. Anger vilken typ av fält källfältet är. Tillgängliga alternativ är: <ul><li>`"text/x.schema-path"` när källfältet är ett fördefinierat XDM-attribut</li><li>`"text/x.aep-xl"` när källfältet är en funktion, till exempel om du behöver ett villkor som ska uppfyllas på källfältets sida. Mer information om funktioner som stöds finns i [Dataprep](/help/data-prep/api/functions.md) dokumentation.</li></ul> |
| `requiredMappings.source` | Sträng | Anger vad det obligatoriska källfältet ska vara. |
| `requiredMappings.destination` | Sträng | Anger vad det obligatoriska målfältet ska vara. |

{style=&quot;table-layout:auto&quot;}

## Identiteter och attribut {#identities-and-attributes}

Parametrarna i det här avsnittet avgör vilka identiteter som ditt mål accepterar. Den här konfigurationen fyller även i målidentiteterna och -attributen i [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i användargränssnittet i Experience Platform, där användare mappar identiteter och attribut från sina XDM-scheman till schemat i målet.


```json
"identityNamespaces": {
        "crm_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Du måste ange vilken [!DNL Platform] identiteter som kunder kan exportera till ditt mål. Några exempel är [!DNL Experience Cloud ID], hashad e-post, enhets-ID ([!DNL IDFA], [!DNL GAID]). Dessa värden är [!DNL Platform] ID-namnutrymmen som kunder kan mappa till identitetsnamnutrymmen från destinationen. Du kan även ange om kunderna kan mappa anpassade namnutrymmen till identiteter som stöds av ditt mål.

Identitetsnamnutrymmen kräver ingen 1-till-1-korrespondens mellan [!DNL Platform] och destinationen.
Kunder kan till exempel mappa en [!DNL Platform] [!DNL IDFA] namnutrymme till ett [!DNL IDFA] namnutrymme från målet eller så kan de mappa samma [!DNL Platform] [!DNL IDFA] namnutrymme till en [!DNL Customer ID] namnutrymme i målet.

## Batchkonfiguration - Namnge filer och schemaläggning av export {#batch-configuration}

Det här avsnittet avser inställningarna för filnamngivning och exportschemaläggning som visas för destinationen i Adobe Experience Platform användargränssnitt. Värdena som du ställer in här visas i [Schemalägg segmentexport](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) steg i det filbaserade arbetsflödet för målaktivering.

```json
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
   }
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolean | Ange till `true` så att kunderna kan ange vilka profilattribut som är obligatoriska. Standardvärdet är `false`. Se [Obligatoriska attribut](../ui/activate-batch-profile-destinations.md#mandatory-attributes) för mer information. |
| `allowDedupeKeyFieldSelection` | Boolean | Ange till `true` så att kunderna kan ange dedupliceringsnycklar. Standardvärdet är `false`.  Se [Dedupliceringsnycklar](../ui/activate-batch-profile-destinations.md#deduplication-keys) för mer information. |
| `defaultExportMode` | Enum | Definierar standardläget för filexport. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Standardvärdet är `DAILY_FULL_EXPORT`. Se [batchaktiveringsdokumentation](../ui/activate-batch-profile-destinations.md#scheduling) om du vill ha mer information om schemaläggning av filexport. |
| `allowedExportModes` | Lista | Definierar vilka filexportlägen som är tillgängliga för kunderna. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Definierar den filexportfrekvens som är tillgänglig för kunder. Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definierar standardexportfrekvensen för filer.Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Standardvärdet är `DAILY`. |
| `defaultStartTime` | Sträng | Definierar standardstarttiden för filexporten. Använder 24-timmars filformat. Standardvärdet är &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Sträng | *Obligatoriskt*. Lista över tillgängliga filnamnsmappar som användare kan välja mellan. Detta avgör vilka objekt som läggs till i de exporterade filnamnen (segment-ID, organisationsnamn, exportdatum och exporttid med mera). Vid inställning `defaultFilename`bör du se till att du inte duplicerar makron. <br><br>Värden som stöds: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Oavsett i vilken ordning du definierar makrona visas de alltid i den ordning som de anges här i användargränssnittet för Experience Platform. <br><br> If `defaultFilename` är tom, `allowedFilenameAppendOptions` listan måste innehålla minst ett makro. |
| `filenameConfig.defaultFilenameAppendOptions` | Sträng | *Obligatoriskt*. Förvalda standardmakron för filnamn som användare kan avmarkera.<br><br> Makrona i den här listan är en delmängd av de som definieras i `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Sträng | *Valfritt*. Definierar standardmakron för filnamn för de exporterade filerna. Användarna kan inte skriva över dem. <br><br>Alla makron som definieras av `allowedFilenameAppendOptions` läggs till efter `defaultFilename` makron. <br><br>If `defaultFilename` är tom, du måste definiera minst ett makro i `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### Filnamnskonfiguration {#file-name-configuration}

Använd konfigurationsmakron för filnamn för att definiera vad de exporterade filnamnen ska innehålla. Makrona i tabellen nedan beskriver element som finns i användargränssnittet i [filnamnskonfiguration](../ui/activate-batch-profile-destinations.md#file-names) skärm.


>[!TIP]
> 
>Som en god praxis bör du alltid inkludera `SEGMENT_ID` makro i de exporterade filnamnen. Segment-ID:n är unika, så om du tar med dem i filnamnet är det bästa sättet att se till att filnamnen också är unika.

| Makro | Gränssnittsetikett | Beskrivning | Exempel |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Målnamn i användargränssnittet. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment ID] | Unikt, plattformsgenererat segment-ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segment Name] | Användardefinierat segmentnamn | VIP prenumerant |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Destination ID] | Unikt, plattformsgenererat ID för målinstansen | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Destination Name] | Användardefinierat namn för målinstansen. | Mål för min 2022-annons |
| `ORGANIZATION_NAME` | [!UICONTROL Organization Name] | Namn på kundorganisationen i Adobe Experience Platform. | Organisationsnamn |
| `SANDBOX_NAME` | [!UICONTROL Sandbox Name] | Namn på den sandlåda som används av kunden. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date and time] | `DATETIME` och `TIMESTAMP` båda definierar när filen skapades, men i olika format. <br><br><ul><li>`DATETIME` använder följande format: YYYMMDD_HMMSS.</li><li>`TIMESTAMP` använder det 10-siffriga Unix-formatet. </li></ul> `DATETIME` och `TIMESTAMP` utesluter varandra och kan inte användas samtidigt. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Custom text] | Användardefinierad egen text som ska inkluderas i filnamnet. Kan inte användas i `defaultFilename`. | Min_egen_text |
| `TIMESTAMP` | [!UICONTROL Date and time] | 10-siffrig tidsstämpel i Unix-format för den tid då filen skapades. | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![Användargränssnittsbild som visar konfigurationsskärmen för filnamn med förvalda makron](assets/file-name-configuration.png)

Exemplet som visas i bilden ovan använder följande makrokonfiguration för filnamn:

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## Krav på historisk profil {#profile-backfill}

Du kan använda `backfillHistoricalProfileData` -parametern i destinationskonfigurationen för att avgöra om historiska profilkvalifikationer ska exporteras till destinationen.

```json
   "backfillHistoricalProfileData":true
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`: [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`: [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Så här ansluter den här konfigurationen all nödvändig information för ditt mål {#connecting-all-configurations}

Vissa av målinställningarna måste konfigureras via [målserver](./server-and-file-configuration.md) eller [konfiguration av målets metadata](./audience-metadata-management.md) slutpunkter. Målkonfigurationen som beskrivs här kopplar samman alla dessa inställningar genom att referera till de två andra konfigurationerna enligt följande:

* Använd `destinationServerId` för att referera till målservern och den filmallskonfiguration som har konfigurerats för ditt mål.
* Använd `audienceMetadataId` för att referera till målgruppens metadatakonfiguration.
