---
description: På den här sidan visas och beskrivs stegen för hur du konfigurerar ett filbaserat mål med Destination SDK.
title: Använd Destination SDK för att konfigurera ett filbaserat mål
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 04e4b0f6b6d84d04d0a24a462383420ebd9a2daf
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Använd Destination SDK för att konfigurera ett filbaserat mål

## Översikt {#overview}

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
        "bucketName": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
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
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
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


## Steg 5: Testa destinationen {#test-destination}

När du har konfigurerat målet med hjälp av konfigurationsslutpunkterna i föregående steg kan du använda kommandot [måltestningsverktyg](./file-based-destination-testing-overview.md) för att testa integrationen mellan Adobe Experience Platform och ditt mål.

Som en del av processen för att testa destinationen måste du använda användargränssnittet i Experience Platform för att skapa segment, som du aktiverar för destinationen. Se de två resurserna nedan för instruktioner om hur du skapar segment i Experience Platform:

* [Skapa en dokumentationssida för segment](/help/segmentation/ui/overview.md#create-segment)
* [Skapa en segmentvideogenomgång](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en)

## Steg 6: Publicera destinationen {#publish-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

När du har konfigurerat och testat destinationen använder du [målpublicerings-API](./destination-publish-api.md) för att skicka in din konfiguration till Adobe för granskning.

## Steg 7: Dokumentera destinationen {#document-destination}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Om du är en oberoende programvaruleverantör (ISV) eller systemintegratör (SI) som skapar en [produktionsintegrering](./overview.md#productized-custom-integrations), använder du [självbetjäningsdokumentationsprocess](./docs-framework/documentation-instructions.md) för att skapa en produktdokumentationssida för destinationen i [Experience Platform destinationskatalog](/help/destinations/catalog/overview.md).

## Steg 8: Skicka mål för Adobe granskning {#submit-for-review}

>[!NOTE]
>
>Det här steget är inte nödvändigt om du skapar ett privat mål för eget bruk och inte vill publicera det i målkatalogen för andra kunder.

Innan destinationen kan publiceras i Experience Platform-katalogen och vara synlig för alla Experience Platform-kunder måste du skicka in destinationen för Adobe granskning officiellt. Hitta fullständig information om hur [skicka för granskning en produkterad destination som skapats i Destination SDK](/help/destinations/destination-sdk/submit-destination.md).
