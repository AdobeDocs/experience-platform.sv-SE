---
description: Med den här konfigurationen kan du ange grundläggande information som målnamn, kategori, beskrivning, logotyp och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål.
title: (Beta) Filbaserade alternativ för destinationskonfiguration för Destination SDK
source-git-commit: 5186e90b850f1e75ec358fa01bfb8a5edac29277
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 3%

---

# (Beta) Filbaserad målkonfiguration {#destination-configuration}

## Översikt {#overview}

>[!IMPORTANT]
>
>Filbaserat målstöd i Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Med den här konfigurationen kan du ange viktig information för ditt filbaserade mål, som målnamn, kategori, beskrivning och annat. Inställningarna i den här konfigurationen avgör också hur Experience Platform-användare autentiserar till ditt mål, hur det visas i användargränssnittet i Experience Platform och vilka identiteter som kan exporteras till ditt mål.

Den här konfigurationen kopplar även de andra konfigurationer som krävs för att målet ska fungera - målserver och målgruppsmetadata - till den här konfigurationen. Läs om hur du kan referera till de två konfigurationerna i en [avsnitt längre nedan](./destination-configuration.md#connecting-all-configurations).

Du kan konfigurera funktionerna som beskrivs i det här dokumentet med hjälp av `/authoring/destinations` API-slutpunkt. Läs [Slutpunktsåtgärder för mål-API](./destination-configuration-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Exempel på destinationskonfiguration för Amazon S3 {#batch-example-configuration}

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes": "2000",
   "maxIdentityAttributes": "10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[],
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
   "identityNamespaces": {
        "adobe_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
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
      "allowJoinKeyFieldSelection":true,
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
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00"
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

### Amazon S3-autentisering

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

I exemplet nedan `customerDataFields` kräver att användare anger ett namn för sitt mål och anger [!DNL Amazon S3] namn och mappsökväg samt komprimeringstyp och filformat.

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
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `documentationLink` | Sträng | Refererar till dokumentationssidan i [Målkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) till destinationen. Använd `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, där `YOURDESTINATION` är namnet på destinationen. För ett mål som heter Moviestar använder du `http://www.adobe.com/go/destinations-moviestar-en` |
| `category` | Sträng | Hänvisar till den kategori som tilldelats ditt mål i Adobe Experience Platform. Mer information finns i [Målkategorier](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Använd något av följande värden: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Sträng | Den URL där du var värd för ikonen som ska visas på målkatalogkortet. |
| `connectionType` | Sträng | Vilken typ av anslutning det är, beroende på målet. Värden som stöds: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Boolean | Anger om målanslutningen ingår i [flödeskörningsgränssnitt](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). När inställningen är `true`: <ul><li>The **[!UICONTROL Last dataflow run date]** och **[!UICONTROL Last dataflow run status]** visas i målbläddringssidan.</li><li>The **[!UICONTROL Dataflow runs]** och **[!UICONTROL Activation data]** -flikar visas på målvysidan.</li></ul> |
| `monitoringSupported` | Boolean | Anger om målanslutningen ingår i [övervakningsgränssnitt](../ui/destinations-workspace.md#browse). När inställningen är `true`, **[!UICONTROL View in monitoring]** -alternativet visas på målbläddringssidan. |
| `frequency` | Sträng | Hänvisar till den typ av dataexport som stöds av målet. Ange till `Batch` för filbaserade mål. |

{style=&quot;table-layout:auto&quot;}

## Destinationsleverans {#destination-delivery}

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
| `destinationServerId` | Sträng | The `instanceId` i [målserverkonfiguration](./destination-server-api.md) används för detta mål. |

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

Använd parametrarna i `schemaConfig` för att aktivera mappningssteget i arbetsflödet för målaktivering. Genom att använda de parametrar som beskrivs nedan kan du bestämma om användare av Experience Platform kan mappa profilattribut och/eller identiteter till ditt filbaserade mål.

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
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `profileFields` | Array | När du lägger till fördefinierade `profileFields`kan Experience Platform-användare mappa plattformsattribut till de fördefinierade attributen i målet. |
| `profileRequired` | Boolean | Använd `true` om användare ska kunna mappa profilattribut från Experience Platform till anpassade attribut på målsidan, vilket visas i exempelkonfigurationen ovan. |
| `segmentRequired` | Boolean | Använd alltid `segmentRequired:true`. |
| `identityRequired` | Boolean | Använd `true` om användare ska kunna mappa identitetsnamnutrymmen från Experience Platform till det önskade schemat. |

{style=&quot;table-layout:auto&quot;}

### Dynamisk schemakonfiguration i mappningssteget {#dynamic-schema-configuration}

Adobe Experience Platform Destination SDK stöder partnerdefinierade scheman. Med ett partnerdefinierat schema kan användare mappa profilattribut och identiteter till anpassade scheman som definierats av målpartners, ungefär som med [mål för direktuppspelning](destination-configuration.md#schema-configuration) arbetsflöde.

Använd parametrarna i  `dynamicSchemaConfig` för att definiera ett eget schema som plattformsprofilattribut och/eller identiteter kan mappas till.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}",
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
| `destinationServerId` | Sträng | The `instanceId` i [målserverkonfiguration](./destination-server-api.md) används för detta mål. |
| `authenticationRule` | Sträng | Anger hur [!DNL Platform] kunderna ansluter till er destination. Godkända värden är `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Använd `CUSTOMER_AUTHENTICATION` om plattformskunder loggar in i systemet på något av följande sätt: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Använd `PLATFORM_AUTHENTICATION` om det finns ett globalt autentiseringssystem mellan Adobe och destinationen och [!DNL Platform] Kunden behöver inte ange några autentiseringsuppgifter för att ansluta till ditt mål. I det här fallet måste du skapa ett autentiseringsobjekt med [Autentiseringsuppgifter](./credentials-configuration-api.md) konfiguration. </li><li>Använd `NONE` om ingen autentisering krävs för att skicka data till målplattformen. </li></ul> |
| `value` | Sträng | Namnet på det schema som ska visas i användargränssnittet i Experience Platform i mappningssteget. |
| `responseFormat` | Sträng | Alltid inställt på `SCHEMA` när du definierar ett anpassat schema. |

{style=&quot;table-layout:auto&quot;}

## Identiteter och attribut {#identities-and-attributes}

Parametrarna i det här avsnittet avgör vilka identiteter som ditt mål accepterar. Den här konfigurationen fyller även i målidentiteterna och -attributen i [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i användargränssnittet i Experience Platform, där användare mappar identiteter och attribut från sina XDM-scheman till schemat i målet.


```json
"identityNamespaces": {
        "adobe_id": {
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

## Batchkonfiguration {#batch-configuration}

I det här avsnittet hänvisas till de inställningar för filexport i konfigurationen ovan som Adobe ska använda för ditt mål i Adobe Experience Platform användargränssnitt.

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
         "ONCE",
         "EVERY_HOUR"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00"
   }
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolean | Ange till `true` så att kunderna kan ange vilka profilattribut som är obligatoriska. Standardvärdet är `false`. Se [Obligatoriska attribut](../ui/activate-batch-profile-destinations.md#mandatory-attributes) för mer information. |
| `allowDedupeKeyFieldSelection` | Boolean | Ange till `true` så att kunderna kan ange dedupliceringsnycklar. Standardvärdet är `false`.  Se [Dedupliceringsnycklar](../ui/activate-batch-profile-destinations.md#deduplication-keys) för mer information. |
| `defaultExportMode` | Enum | Definierar standardläget för filexport. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul><br> Standardvärdet är `DAILY_FULL_EXPORT`. Se [batchaktiveringsdokumentation](../ui/activate-batch-profile-destinations.md#scheduling) om du vill ha mer information om schemaläggning av filexport. |
| `allowedExportModes` | Lista | Definierar vilka filexportlägen som är tillgängliga för kunderna. Värden som stöds:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Definierar den filexportfrekvens som är tillgänglig för kunder. Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definierar standardexportfrekvensen för filer.Värden som stöds:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> <br> Standardvärdet är `DAILY`. |
| `defaultStartTime` | Sträng | Definierar standardstarttiden för filexporten. Använder 24-timmars filformat. Standardvärdet är &quot;00:00&quot;. |

## Krav på historisk profil {#profile-backfill}

Du kan använda `backfillHistoricalProfileData` -parametern i destinationskonfigurationen för att avgöra om historiska profilkvalifikationer ska exporteras till destinationen.

```json
   "backfillHistoricalProfileData":true
```

| Parameter | Typ | Beskrivning |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolean | Anger om historiska profildata exporteras när segment aktiveras till målet. <br> <ul><li> `true`: [!DNL Platform] skickar de historiska användarprofiler som är kvalificerade för segmentet innan segmentet aktiveras. </li><li> `false`: [!DNL Platform] innehåller endast användarprofiler som är kvalificerade för segmentet efter att segmentet har aktiverats. </li></ul> |

## Så här ansluter den här konfigurationen all nödvändig information för ditt mål {#connecting-all-configurations}

Vissa av målinställningarna måste konfigureras via [målserver](./server-and-file-configuration.md) eller [konfiguration av målets metadata](./audience-metadata-management.md). Målkonfigurationen som beskrivs här kopplar samman alla dessa inställningar genom att referera till de två andra konfigurationerna enligt följande:

* Använd `destinationServerId` för att referera till målservern och mallkonfigurationen som har konfigurerats för ditt mål.
* Använd `audienceMetadataId` för att referera till målgruppens metadatakonfiguration.
