---
description: Lär dig hur du använder Destination SDK för att konfigurera ett SFTP-mål med fördefinierade filformateringsalternativ och en anpassad filnamnskonfiguration.
title: Konfigurera ett SFTP-mål med fördefinierade filformateringsalternativ och anpassad filnamnskonfiguration.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Konfigurera ett SFTP-mål med fördefinierade filformateringsalternativ och anpassad filnamnskonfiguration

## Översikt {#overview}

På den här sidan beskrivs hur du använder Destination SDK för att konfigurera ett SFTP-mål med fördefinierade standardalternativ för [filformatering](configure-file-formatting-options.md) och en anpassad [filnamnskonfiguration](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

På den här sidan visas alla konfigurationsalternativ som är tillgängliga för SFTP-mål. Du kan redigera konfigurationerna som visas i stegen nedan eller ta bort vissa delar av konfigurationerna efter behov.

Detaljerade beskrivningar av parametrarna som används nedan finns i [konfigurationsalternativ i Destinations SDK](../../functionality/configuration-options.md).

## Förhandskrav {#prerequisites}

Innan du går vidare till stegen som beskrivs nedan bör du läsa sidan [Komma igång för Destination SDK](../../getting-started.md) för att få information om hur du får de autentiseringsuppgifter för Adobe I/O och andra krav som krävs för att arbeta med Destination SDK-API:er.

## Steg 1: Skapa en server- och filkonfiguration {#create-server-file-configuration}

Börja med att använda slutpunkten `/destination-server` för att [skapa en server- och filkonfiguration](../../authoring-api/destination-server/create-destination-server.md).

**API-format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Begäran**

Följande begäran skapar en ny målserverkonfiguration, konfigurerad med parametrarna som anges i nyttolasten.
Nyttolasten nedan innehåller en allmän SFTP-konfiguration med fördefinierade, standardinställda [CSV-filformateringsparametrar](../../functionality/destination-server/file-formatting.md) som användare kan definiera i användargränssnittet för Experience Platform.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}'
```

Ett lyckat svar returnerar den nya målserverkonfigurationen, inklusive konfigurationens unika identifierare (`instanceId`). Lagra det här värdet som det ska i nästa steg.

## Steg 2: Skapa målkonfiguration {#create-destination-configuration}

När du har skapat målservern och filformateringskonfigurationen i föregående steg kan du nu använda API-slutpunkten `/destinations` för att skapa en målkonfiguration.

Om du vill ansluta serverkonfigurationen i [steg 1](#create-server-file-configuration) till den här målkonfigurationen ersätter du värdet `destinationServerId` i API-begäran nedan med värdet som du fick när du skapade målservern i [steg 1](#create-server-file-configuration).

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
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
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
         "destinationServerId":"{{instanceID of your destination server}}"
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

Ett lyckat svar returnerar den nya målkonfigurationen, inklusive konfigurationens unika identifierare (`instanceId`). Lagra det här värdet som det är nödvändigt om du behöver göra ytterligare HTTP-begäranden för att uppdatera målkonfigurationen.

## Steg 3: Verifiera användargränssnittet i Experience Platform {#verify-ui}

Baserat på ovanstående konfigurationer kommer Experience Platform-katalogen nu att visa ett nytt privat destinationskort som du kan använda.

![Skärminspelning som visar målkatalogsidan med ett valt målkort.](../../assets/guides/batch/destination-card.gif)

Observera hur alternativen i [aktiveringsarbetsflödet för filbaserade mål](/help/destinations/ui/activate-batch-profile-destinations.md) i bilderna och inspelningarna nedan matchar alternativen som du valde i målkonfigurationen.

När du fyller i information om målet bör du tänka på hur fälten som visas är anpassade datafält som du ställer in i konfigurationen.

>[!TIP]
>
>Den ordning i vilken du lägger till anpassade datafält i målkonfigurationen visas inte i användargränssnittet. De anpassade datafälten visas alltid i den ordning som visas i skärminspelningen nedan.

![fyll i målinformation](../../assets/guides/batch/file-configuration-options.gif)

När du schemalägger exportintervall bör du observera hur fälten som visas är de fält som du har konfigurerat i `batchConfig`-konfigurationen.
![alternativ för exportplanering](../../assets/guides/batch/file-export-scheduling.png)

När du visar konfigurationsalternativen för filnamn bör du observera hur fälten som visas representerar de `filenameConfig`-alternativ som du har konfigurerat i konfigurationen.
![konfigurationsalternativ för filnamn](../../assets/guides/batch/file-naming-options.gif)

Om du vill justera något av fälten ovan upprepar du [steg ett](#create-server-file-configuration) och [två](#create-destination-configuration) för att ändra konfigurationerna efter dina behov.

## Steg 4: (Valfritt) Publish ditt mål {#publish-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

När du har konfigurerat målet kan du använda [API:t för målpublicering](../../publishing-api/create-publishing-request.md) för att skicka konfigurationen till Adobe för granskning.

## Steg 5: (Valfritt) Dokumentera destinationen {#document-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [tillverkad integrering](../../overview.md#productized-custom-integrations) använder du [självbetjäningsdokumentationsprocessen](../../docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience Platform-målkatalogen](../../../catalog/overview.md).

## Nästa steg {#next-steps}

Genom att läsa den här artikeln vet du nu hur du skapar ett anpassat SFTP-mål med hjälp av Destination SDK. Därefter kan ditt team använda [aktiveringsarbetsflödet för filbaserade mål](../../../ui/activate-batch-profile-destinations.md) för att exportera data till målet.
