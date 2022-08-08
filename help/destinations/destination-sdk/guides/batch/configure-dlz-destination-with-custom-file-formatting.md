---
description: Lär dig hur du använder Destination SDK för att konfigurera ett DLZ-mål (Data Landing Zone) med anpassade filformateringsalternativ och anpassad filnamnskonfiguration.
title: (Beta) Konfigurera ett DLZ-mål (Data Landing Zone) med anpassade filformateringsalternativ och anpassad filnamnskonfiguration.
source-git-commit: fd3114a4578637dcf99232245f8d2cec64de14b5
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# (Beta) Konfigurera en [!DNL Data Landing Zone (DLZ)] mål med anpassade filformateringsalternativ och anpassad filnamnskonfiguration

## Översikt {#overview}

>[!IMPORTANT]
>
>Funktionen för att konfigurera filbaserade mål med Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

På den här sidan beskrivs hur du använder Destination SDK för att konfigurera en [!DNL Data Landing Zone] mål med anpassad [filformateringsalternativ](../../server-and-file-configuration.md#file-configuration) och en egen [filnamnskonfiguration](../../file-based-destination-configuration.md#file-name-configuration).

På den här sidan visas alla konfigurationsalternativ som är tillgängliga för [!DNL Data Landing Zone] destinationer. Du kan redigera konfigurationerna som visas i stegen nedan eller ta bort vissa delar av konfigurationerna efter behov.

## Förutsättningar {#prerequisites}

Innan du går vidare till stegen nedan ska du läsa [Komma igång med Destination SDK](../../getting-started.md) för information om hur du får de autentiseringsuppgifter för Adobe I/O och andra krav som krävs för att arbeta med Destination SDK-API:er.

## Steg 1: Skapa en server- och filkonfiguration {#create-server-file-configuration}

Börja med att använda `/destination-server` slutpunkt för att skapa en server- och filkonfiguration. Mer information om parametrarna i HTTP-begäran finns i [server- och filkonfigurationsspecifikationer för filbaserade mål](../../server-and-file-configuration.md#adls-example) och associerade [filformateringskonfigurationer](../../server-and-file-configuration.md#file-configuration).

**API-format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Begäran**

Följande begäran skapar en ny målserverkonfiguration, konfigurerad med parametrarna som anges i nyttolasten.
Nedan finns en allmän [!DNL Data Landing Zone] konfiguration, med anpassad [CSV-filformatering](../../server-and-file-configuration.md#file-configuration) konfigurationsparametrar som användare kan definiera i användargränssnittet för Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
 -d '
{
   "name":"DLZ Destination Server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "fileConfigurations":{
         "compression":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.compression}}"
         },
         "fileType":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.fileType}}"
         },
         "csvOptions":{
            "sep":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.sep}}"
            },
            "encoding":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.encoding}}"
            },
            "quote":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quote}}"
            },
            "quoteAll":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.quoteAll}}"
            },
            "escape":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escape}}"
            },
            "escapeQuotes":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.escapeQuotes}}"
            },
            "header":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.header}}"
            },
            "ignoreLeadingWhiteSpace":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.ignoreLeadingWhiteSpace}}"
            },
            "nullValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.nullValue}}"
            },
            "dateFormat":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            },
            "charToEscapeQuoteEscaping":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.charToEscapeQuoteEscaping}}"
            },
            "emptyValue":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.dateFormat}}"
            }
         }
      }
   }
}'
```

Ett lyckat svar returnerar den nya målserverkonfigurationen, inklusive den unika identifieraren (`instanceId`) av konfigurationen. Lagra det här värdet som det ska i nästa steg.

## Steg 2: Skapa målkonfiguration {#create-destination-configuration}

När du har skapat målservern och filformateringskonfigurationen i föregående steg kan du nu använda `/destinations` API-slutpunkt för att skapa en målkonfiguration.

Ansluta serverkonfigurationen i [steg 1](#create-server-file-configuration) till den här målkonfigurationen, ersätt `destinationServerId` värdet i API-begäran nedan med värdet som du fick när du skapade målservern i [steg 1](#create-server-file-configuration).

Detaljerade beskrivningar av parametrarna nedan finns på följande sidor:

* [Autentiseringskonfiguration](../../authentication-configuration.md#adls)
* [Konfiguration av batchmål](../../file-based-destination-configuration.md#batch-configuration)
* [Filbaserade API-åtgärder för målkonfiguration](../../destination-configuration-api.md#create-file-based)

**API-format**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Begäran**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ Destination",
   "description":"SSD DLZ Destination",
   "releaseNotes":"Test release notes for DLZ Destination",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
       
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"path",
         "title":"Folder path",
         "description":"Enter the path to your Data Landing Zone folder",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
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
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
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
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
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
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
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
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
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
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
         "title":"File type",
         "description":"Select the exported file type.",
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
      "documentationLink":"https://www.adobe.io/apis/experienceplatform.html",
      "category":"DLZ",
      "connectionType":"Server-to-server",
      "frequency":"Batch",
      "flowRunsSupported":true,
      "monitoringSupported":true
   },
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
      "mapUserInput":false
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
         "authenticationRule":"NONE",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "identityRequired":true,
      "segmentRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "autoSelectJoinKeyOnPartnerSchemaSelection":false,
      "joinKeyTitle":"DEDUPLICATION KEY",
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportModes":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_12_HOURS",
         "EVERY_8_HOURS",
         "ONCE",
         "EVERY_HOUR"
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
      "allowDedupKeyFieldSelection":true
   },
   "backfillHistoricalProfileData":true
}'
```

Ett lyckat svar returnerar den nya målkonfigurationen, inklusive den unika identifieraren (`instanceId`) av konfigurationen. Lagra det här värdet som det är nödvändigt om du behöver göra ytterligare HTTP-begäranden för att uppdatera målkonfigurationen.

## Steg 3: Verifiera användargränssnittet i Experience Platform {#verify-ui}

Baserat på ovanstående konfigurationer kommer Experience Platform-katalogen nu att visa ett nytt privat destinationskort som du kan använda.

![Skärminspelning som visar målkatalogsidan med ett valt målkort.](../../assets/dlz-destination-card.gif)

Observera hur alternativen i [aktiveringsarbetsflöde för filbaserade mål](/help/destinations/ui/activate-batch-profile-destinations.md) matchar alternativen som du valde i målkonfigurationen.

När du fyller i information om målet bör du tänka på hur fälten som visas är anpassade datafält som du ställer in i konfigurationen.

>[!TIP]
>
>Den ordning i vilken du lägger till anpassade datafält i målkonfigurationen visas inte i användargränssnittet. De anpassade datafälten visas alltid i den ordning som visas i skärminspelningen nedan.

![fylla i målinformation](../../assets/file-configuration-options.gif)

När du schemalägger exportintervall bör du tänka på hur fälten visas i `batchConfig` konfiguration.
![alternativ för exportplanering](../../assets/file-export-scheduling.png)

När du visar alternativen för filnamnskonfiguration bör du tänka på hur fälten som visas representerar `filenameConfig` alternativ som du ställer in i konfigurationen.
![konfigurationsalternativ för filnamn](../../assets/file-naming-options.gif)

Om du vill justera något av de fält som nämns ovan upprepar du [steg ett](#create-server-file-configuration) och [två](#create-destination-configuration) för att ändra konfigurationerna efter dina behov.

## Steg 4: (Valfritt) Publicera destinationen {#publish-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

När du har konfigurerat målet använder du [målpublicerings-API](../../destination-publish-api.md) för att skicka in din konfiguration till Adobe för granskning.

## Steg 5: (Valfritt) Dokumentera destinationen {#document-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktionsintegrering](../../overview.md#productized-custom-integrations), använder du [självbetjäningsdokumentationsprocess](../../docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience Platform destinationskatalog](../../../catalog/overview.md).

## Nästa steg {#next-steps}

Genom att läsa den här artikeln kan du nu skapa en egen [!DNL Data Landing Zone] mål genom att använda Destination SDK. Sedan kan ditt team använda [aktiveringsarbetsflöde för filbaserade mål](../../../ui/activate-batch-profile-destinations.md) för att exportera data till målet.
