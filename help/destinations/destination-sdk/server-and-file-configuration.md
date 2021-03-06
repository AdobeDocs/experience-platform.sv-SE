---
description: Server- och filkonfigurationsspecifikationerna för filbaserade mål kan konfigureras i Adobe Experience Platform Destination SDK via slutpunkten /destination-servers.
title: (Beta) Konfigurationsalternativ för filbaserade målserverspecifikationer
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 7a72c190d28d63c7bcd1bf12d8a52efc4589b848
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 8%

---

# (Beta) Server- och filkonfiguration för filbaserade målserverspecifikationer

## Översikt {#overview}

>[!IMPORTANT]
>
>Funktionen för att konfigurera och skicka filbaserade mål med Adobe Experience Platform Destination SDK finns för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

På den här sidan beskrivs alla serverkonfigurationsalternativ för de filbaserade målservrarna och du får instruktioner om hur du ställer in olika filkonfigurationsalternativ för användare som exporterar filer från Experience Platform till målet.

Server- och filkonfigurationsspecifikationerna för filbaserade mål kan konfigureras i Adobe Experience Platform Destination SDK via `/destination-servers` slutpunkt. Läs [API-slutpunktsåtgärder för målserver](./destination-server-api.md) för en fullständig lista över åtgärder som du kan utföra på slutpunkten.

## Filbaserad Amazon S3-målserverspecifikation {#s3-example}

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
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Amazon S3], ange detta till `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Sträng | Namnet på [!DNL Amazon S3] bucket som ska användas för detta mål. |
| `fileBasedS3Destination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filbaserad SFTP-målserverspecifikation {#sftp-example}

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL SFTP] mål, ange detta till `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | Sträng | Mållagringens rotkatalog. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | Sträng | Mållagringens värdnamn. |
| `port` | Heltal | SFTP-filserverporten. |
| `encryptionMode` | Sträng | Anger om filkryptering ska användas. Värden som stöds: <ul><li>PGP</li><li>Ingen</li></ul> |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filbaserad [!DNL Azure Data Lake Storage] ([!DNL ADLS]) målserverspecifikation {#adls-example}

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Data Lake Storage] mål, ange detta till `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filbaserad [!DNL Azure Blob Storage] målserverspecifikation {#blob-example}

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Blob Storage] mål, ange detta till `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Sträng | Namnet på [!DNL Azure Blob Storage] behållare som ska användas av det här målet. |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filbaserad [!DNL Data Landing Zone] ([!DNL DLZ]) målserverspecifikation {#dlz-example}

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Data Landing Zone] mål, ange detta till `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filbaserad [!DNL Google Cloud Storage] målserverspecifikation {#gcs-example}

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      // See the file formatting configuration section further below on this page
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Google Cloud Storage] mål, ange detta till `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Sträng | Namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Objekt | Se [filformatskonfiguration](#file-configuration) om du vill ha detaljerade förklaringar om det här avsnittet. |

{style=&quot;table-layout:auto&quot;}

## Filformateringskonfiguration {#file-configuration}

I det här avsnittet beskrivs filformateringsinställningarna för den exporterade `CSV` filer. Du kan ändra flera egenskaper för de exporterade filerna så att de matchar kraven i filmottagningssystemet på din sida för att optimera läsningen och tolkningen av de filer som tas emot från Experience Platform.

>[!NOTE]
>
>CSV-alternativ stöds bara när CSV-filer exporteras. The `fileConfigurations` -avsnittet är inte obligatoriskt när du konfigurerar en ny målserver. Om du inte skickar några värden i API-anropet för CSV-alternativen används standardvärdena från tabellen nedan.

```json
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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        },
        "maxFileRowCount":5000000
    }
```

| Fält | Obligatoriskt/valfritt | Beskrivning | Standardvärde |
|---|---|---|---|
| `compression.value` | Valfritt | Komprimeringskodek som ska användas när data sparas i en fil. Värden som stöds: `none`, `bzip2`, `gzip`, `lz4`och `snappy`. | `none` |
| `fileType.value` | Valfritt | Anger utdatafilens format. Värden som stöds: `csv`, `parquet`och `json`. | `csv` |
| `csvOptions.quote.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger ett enskilt tecken som används för att undvika citattecken där avgränsaren kan vara en del av värdet. | `null` |
| `csvOptions.quoteAll.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om alla värden alltid ska omslutas av citattecken. Som standard är det bara escape-värden som innehåller ett citattecken. | `false` |
| `csvOptions.escape.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger ett enskilt tecken som används för att undvika citattecken i ett redan citattecken. | `\` |
| `csvOptions.escapeQuotes.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om värden som innehåller citattecken alltid ska omslutas av citattecken. Standard är att undvika alla värden som innehåller ett citattecken. | `true` |
| `csvOptions.header.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om kolumnnamnen ska skrivas som den första raden. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om inledande blanksteg ska trimmas från värden. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om efterföljande blanksteg ska trimmas från värden. | `true` |
| `csvOptions.nullValue.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängbeteckningen för ett null-värde. | `""` |
| `csvOptions.dateFormat.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger datumformatet. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängen som anger ett tidsstämpelformat. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Ställer in ett enda tecken som används för att kringgå citattecknet. | `\` när escape- och citattecknen är olika. `\0` när escape- och citattecknet är detsamma. |
| `csvOptions.emptyValue.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängbeteckningen för ett tomt värde. | `""` |
| `csvOptions.lineSep.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Definierar den radavgränsare som ska användas för skrivning. Maxlängden är 1 tecken. | `\n` |
| `maxFileRowCount` | Valfritt | Maximalt antal rader som den exporterade filen kan innehålla. Konfigurera detta baserat på kraven för målplattformens filstorlek. | Ej tillämpligt |

{style=&quot;table-layout:auto&quot;}