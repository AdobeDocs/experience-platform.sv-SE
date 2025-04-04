---
description: På den här sidan visas ett exempel på det API-anrop som används för att uppdatera en befintlig målkonfiguration via Adobe Experience Platform Destination SDK.
title: Uppdatera en målkonfiguration
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 163c6f6bacfd6f0928b1053bd146a2d4fc4c74d0
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Uppdatera en målkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att uppdatera en befintlig målkonfiguration med API-slutpunkten `/authoring/destinations`.

>[!TIP]
>
>Alla uppdateringsåtgärder på produkterade/publika mål visas först när du har använt [publicerings-API](../../publishing-api/create-publishing-request.md) och skickat uppdateringen för Adobe granskning.

En detaljerad beskrivning av funktionerna i en målkonfiguration finns i följande artiklar:

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

## Uppdatera en målkonfiguration {#update}

Du kan uppdatera en [befintlig](create-destination-configuration.md) målkonfiguration genom att göra en `PUT`-begäran till `/authoring/destinations`-slutpunkten med den uppdaterade nyttolasten.

>[!TIP]
>
>API-slutpunkt: `platform.adobe.io/data/core/activation/authoring/destinations`

Om du vill hämta en befintlig målkonfiguration och dess motsvarande `{INSTANCE_ID}` läser du artikeln om [att hämta en målkonfiguration](retrieve-destination-configuration.md).

**API-format**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målkonfigurationen som du vill uppdatera. Information om hur du hämtar en befintlig målkonfiguration och dess motsvarande `{INSTANCE_ID}` finns i [Hämta en målkonfiguration](retrieve-destination-configuration.md). |

+++Begäran

Följande begäran uppdaterar målet som vi skapade i [det här exemplet](create-destination-configuration.md#create) med olika `filenameConfig` alternativ.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
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
   "customerEncryptionConfigurations":[
       
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målkonfigurationen.

+++

## API-felhantering {#error-handling}

Destination SDK API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för Experience Platform.

## Nästa steg

När du har läst det här dokumentet vet du nu hur du uppdaterar en målkonfiguration via API-slutpunkten för Destination SDK `/authoring/destinations`.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Skapa en målkonfiguration](create-destination-configuration.md)
* [Hämta en målkonfiguration](retrieve-destination-configuration.md)
* [Ta bort en målkonfiguration](delete-destination-configuration.md)
