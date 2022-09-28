---
description: På den här sidan visas och beskrivs stegen för hur du konfigurerar ett filbaserat mål med Destination SDK.
title: Använd Destination SDK för att konfigurera ett filbaserat mål
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Använd Destination SDK för att konfigurera ett filbaserat mål

## Översikt {#overview}

>[!IMPORTANT]
>
>Funktionen för att konfigurera och skicka filbaserade mål med Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Den här sidan beskriver hur du använder informationen i [Konfigurationsalternativ i mål-SDK](./configuration-options.md) och i andra Destinationer SDK och API-referensdokument för att konfigurera [filbaserat mål](../../destinations/destination-types.md#file-based). Stegen beskrivs i sekventiell ordning nedan.

## Förutsättningar {#prerequisites}

Innan du går vidare till stegen som visas nedan ska du läsa [Komma igång med Destination SDK](./getting-started.md) för information om hur du får de autentiseringsuppgifter för Adobe I/O och andra krav som krävs för att arbeta med Destination SDK-API:er.

## Steg för att använda konfigurationsalternativen i Destinationen SDK för att konfigurera destinationen {#steps}

![Illustrerade steg för att använda Destinationens SDK slutpunkter](./assets/destination-sdk-steps-batch.png)

## Steg 1: Skapa en server- och filkonfiguration {#create-server-file-configuration}

Börja med att skapa en server- och filkonfiguration med `/destinations-server` slutpunkt (läs [API-referens](./destination-server-api.md)).

Nedan visas ett exempel på en konfiguration för en [!DNL Amazon S3] mål. Om du vill konfigurera andra typer av filbaserade mål läser du i motsvarande [serverkonfigurationer](server-and-file-configuration.md).

**API-format**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
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
}
```

## Steg 2: Skapa målkonfiguration {#create-destination-configuration}

Nedan visas ett exempel på en destinationskonfiguration som skapats med `/destinations` API-slutpunkt. Mer information om den här konfigurationen finns i [Målkonfiguration](./file-based-destination-configuration.md).

Om du vill ansluta server- och filkonfigurationen i steg 1 till den här målkonfigurationen lägger du till instans-ID:t för servern och mallkonfigurationen som `destinationServerId` här.

**API-format**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
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
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## Steg 3: Skapa konfiguration för målgruppsmetadata {#create-audience-metadata-configuration}

För vissa destinationer kräver Destinationen SDK att du konfigurerar en målgruppsmetadatakonfiguration för att skapa, uppdatera eller ta bort målgrupper i målgruppen. Se [Hantering av målgruppsmetadata](./audience-metadata-management.md) om du vill ha information om när du behöver konfigurera den här konfigurationen och hur du gör det.

Om du använder en konfiguration för målgruppsmetadata måste du ansluta den till målkonfigurationen som du skapade i steg 2. Lägg till instans-ID:t för målgruppens metadatakonfiguration i målkonfigurationen som `audienceTemplateId`.

## Steg 4: Konfigurera autentisering {#set-up-authentication}

Beroende på om du anger `"authenticationRule": "CUSTOMER_AUTHENTICATION"` eller `"authenticationRule": "PLATFORM_AUTHENTICATION"` i målkonfigurationen ovan kan du konfigurera autentisering för målet med hjälp av `/destination` eller `/credentials` slutpunkt.

* Om du valde `"authenticationRule": "CUSTOMER_AUTHENTICATION"` i målkonfigurationen, se följande avsnitt för de autentiseringstyper som stöds av Destinationen SDK för filbaserade mål:

   * [Amazon S3-autentisering](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure Data Lake-lagring](authentication-configuration.md#adls)
   * [Google Cloud-lagring](authentication-configuration.md#gcs)
   * [SFTP-autentisering med SSH-nyckel](authentication-configuration.md#sftp-ssh)
   * [SFTP-autentisering med lösenord](authentication-configuration.md#sftp-password)

* Om du valde `"authenticationRule": "PLATFORM_AUTHENTICATION"`, se [Autentiseringskonfiguration](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## Steg 5: Publicera destinationen {#publish-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

När du har konfigurerat och testat destinationen använder du [målpublicerings-API](./destination-publish-api.md) för att skicka in din konfiguration till Adobe för granskning.

## Steg 6: Dokumentera destinationen {#document-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktionsintegrering](./overview.md#productized-custom-integrations), använder du [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience Platform destinationskatalog](/help/destinations/catalog/overview.md).
