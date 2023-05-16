---
description: Lär dig hur du konfigurerar målserverspecifikationer i Adobe Experience Platform Destination SDK via slutpunkten "/authoring/destination-servers".
title: Serverspecifikationer för mål som skapats med Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 2%

---


# Serverspecifikationer för mål som skapats med Destination SDK

Målserverns specifikationer definierar vilken typ av målplattform som ska ta emot data från Adobe Experience Platform och kommunikationsparametrarna mellan plattformen och destinationen. Till exempel:

* A [direktuppspelning](#streaming-example) målserverspecifikationen definierar HTTP-serverslutpunkten som tar emot HTTP-meddelanden från plattformen. Läs mer om hur du konfigurerar hur HTTP-anrop till slutpunkten formateras i [mallange specifikationer](templating-specs.md) sida.
* An [Amazon S3](#s3-example) målserverspecifikationen definierar [!DNL S3] namn och sökväg där Plattform exporterar filerna.
* An [SFTP](#sftp-example) målserverspecifikationen definierar värdnamnet, rotkatalogen, kommunikationsporten och krypteringstypen för SFTP-servern där plattformen ska exportera filerna.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se följande sidor med översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Du kan konfigurera målserverns specifikationer via `/authoring/destination-servers` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Uppdatera en målserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

På den här sidan visas alla målservertyper som stöds av Destinationen SDK, med alla deras konfigurationsparametrar. Ersätt parametervärdena med dina egna när du skapar målet.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

När [skapa](../../authoring-api/destination-server/create-destination-server.md) eller [uppdatera](../../authoring-api/destination-server/update-destination-server.md) en målserver använder du någon av de servertypskonfigurationer som beskrivs på den här sidan. Beroende på dina integrationskrav ska du se till att ersätta exempelparametervärdena från de här exemplen med dina egna.

## Hårdkodade jämfört med mallsidesfält {#templatized-fields}

När du skapar en målserver via Destination SDK kan du definiera parametervärden för konfiguration antingen genom att hårdkoda dem i konfigurationen eller genom att använda mallfält. I mallbaserade fält kan du läsa användardefinierade värden från plattformens användargränssnitt.

Målserverparametrar har två konfigurerbara fält. Dessa alternativ avgör om du använder hårdkodade eller mallsidiga värden.

| Parameter | Typ | Beskrivning |
|---|---|---|
| `templatingStrategy` | Sträng | *Obligatoriskt.* Definierar om det finns ett hårdkodat värde via `value` eller ett användarkonfigurerbart värde i användargränssnittet. Värden som stöds: <ul><li>`NONE`: Använd det här värdet när du hårdkodar parametervärdet via `value` parameter (se nästa rad). Exempel:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Använd det här värdet när du vill att användarna ska ange ett parametervärde i användargränssnittet. Exempel: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Sträng | *Obligatoriskt*. Definierar parametervärdet. Värdetyper som stöds: <ul><li>**Hårdkodat värde**: Använd ett hårdkodat värde (till exempel `"value": "my-storage-bucket"`) när du inte behöver att användarna anger ett parametervärde i användargränssnittet. När du hårdkodar ett värde `templatingStrategy` ska alltid anges till `NONE`.</li><li>**Mallvärde**: Använd ett mallsidigt värde (till exempel `"value": "{{customerData.bucket}}"`) när du vill att användarna ska ange ett parametervärde i användargränssnittet. När du använder mallsidesvärden `templatingStrategy` ska alltid anges till `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### När hårdkodade jämfört med mallsidesfält ska användas

Både hårdkodade och mallbaserade fält har sina egna användningsområden i Destinationen SDK, beroende på vilken typ av integrering du skapar.

**Ansluta till målet utan användarindata**

När användare [ansluta till ditt mål](../../../ui/connect-destination.md) i plattformsgränssnittet kanske du vill hantera målanslutningsprocessen utan indata.

Det gör du genom att hårdkoda anslutningsparametrarna för målplattformen i serverspecifikationen. När du använder hårdkodade parametervärden i målserverkonfigurationen hanteras anslutningen mellan Adobe Experience Platform och målplattformen utan indata från användaren.

I exemplet nedan skapar en partner en Data Landing Zone-målserver med `path.value` fält som hårdkodas.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Detta resulterar i att när användare går igenom [självstudiekurs om målanslutning](../../../ui/connect-destination.md), kommer de inte att se [autentiseringssteg](../../../ui/connect-destination.md#authenticate). Autentiseringen hanteras i stället av Platform, vilket visas i bilden nedan.

![Användarbild som visar autentiseringsskärmen mellan plattformen och ett DLZ-mål.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Ansluta till målet med användarindata**

När anslutningen mellan plattformen och målet ska upprättas efter en viss användarinmatning i plattformsgränssnittet, till exempel val av en API-slutpunkt eller tillhandahållande av ett fältvärde, kan du använda mallfält i serverspecifikationen för att läsa användarinmatningen och ansluta till målplattformen.

I exemplet nedan skapar en partner en [realtid (direktuppspelning)](#streaming-example) integrering och `url.value` fältet använder den mallsidiga parametern `{{customerData.region}}` för att anpassa en del av API-slutpunkten baserat på användarindata.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Om du vill att användarna ska kunna välja ett värde i användargränssnittet för plattformen väljer du `region` -parametern måste också definieras i [målkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md) som ett kunddatafält, vilket visas nedan:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Detta resulterar i att när användare går igenom [självstudiekurs om målanslutning](../../../ui/connect-destination.md)måste de välja en region innan de kan ansluta till målplattformen. När de ansluter till målet, det mallsidiga fältet `{{customerData.region}}` ersätts med det värde som användaren har valt i användargränssnittet, vilket visas i bilden nedan.

![Användarbild som visar målanslutningsskärmen med en regionväljare.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Målserver för realtid (direktuppspelning) {#streaming-example}

Med den här målservertypen kan du exportera data från Adobe Experience Platform till målet via HTTP-begäranden. Serverkonfigurationen innehåller information om servern som tar emot meddelandena (servern på din sida).

Den här processen levererar användardata som en serie HTTP-meddelanden till målplattformen. Parametrarna nedan utgör mallen för specifikationer för HTTP-servern.

I exemplet nedan visas ett exempel på en målserverkonfiguration för ett mål för realtidsströmning.

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | *Obligatoriskt.* Representerar ett eget namn på servern som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel: `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Obligatoriskt.* Ange detta till `URL_BASED` för direktuppspelningsmål. |
| `templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om du använder ett mallbaserat fält i stället för ett hårdkodat värde i `value` fält. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items`, där användarna måste välja slutpunktsområdet i plattformsgränssnittet. </li><li> Använd `NONE` om ingen mallad omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |

{style="table-layout:auto"}

## [!DNL Amazon S3] målserver {#s3-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till din Amazon S3-lagring.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett Amazon S3-mål.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målservern. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Exportera filer till en [!DNL Amazon S3] bucket, ställ in det här på `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `bucket.value` fält.<ul><li>Om du vill att användarna ska ange sina egna bucketnamn i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat kryckennamn för din integrering, till exempel `"bucket.value":"MyBucket"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Sträng | Namnet på [!DNL Amazon S3] bucket som ska användas för detta mål. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `path.value` fält.<ul><li>Om du vill att dina användare ska ange en egen sökväg i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `path.value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"bucket.value":"/path/to/MyBucket"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Sträng | Sökvägen till [!DNL Amazon S3] bucket som ska användas för detta mål. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] målserver {#sftp-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till [!DNL SFTP] lagringsserver.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett SFTP-mål.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målservern. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Exportera filer till en [!DNL SFTP] mål, ange detta till `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `rootDirectory.value` fält.<ul><li>Om du vill att användarna ska ange sin egen rotkatalogsökväg i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `rootDirectory.value` fält för att läsa ett användardefinierat värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad rotkatalogsökväg för din integrering, till exempel `"rootDirectory.value":"Storage/MyDirectory"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Sträng | Sökvägen till den katalog som ska vara värd för de exporterade filerna. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `hostName.value` fält.<ul><li>Om du vill att dina användare ska ange sitt eget värdnamn i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `hostName.value` fält för att läsa ett användardefinierat värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat värdnamn för din integrering, till exempel `"hostName.value":"my.hostname.com"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Sträng | Värdnamnet för SFTP-servern. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"hostName.value":"my.hostname.com"`. |
| `port` | Heltal | SFTP-filserverporten. |
| `encryptionMode` | Sträng | Anger om filkryptering ska användas. Värden som stöds: <ul><li>PGP</li><li>Ingen</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) målserver {#adls-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till [!DNL Azure Data Lake Storage] konto.

Exemplet nedan visar ett exempel på en målserverkonfiguration för en [!DNL Azure Data Lake Storage] mål.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Data Lake Storage] mål, ange detta till `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `path.value` fält.<ul><li>Om du vill att dina användare ska ange sina [!DNL ADLS] mappsökväg i användargränssnittet för Experience Platform, ange det här värdet som `PEBBLE_V1`. I det här fallet måste du mallsialisera `path.value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Sträng | Vägen till [!DNL ADLS] lagringsmapp. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] målserver {#blob-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till [!DNL Azure Blob Storage] behållare.

Exemplet nedan visar ett exempel på en målserverkonfiguration för en [!DNL Azure Blob Storage] mål.

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
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Blob Storage] mål, ange detta till `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `path.value` fält.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Azure Blob] [URI för lagringskonto](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `path.value` fält för att läsa värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "https://myaccount.blob.core.windows.net/"`och ange det här värdet till `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Sträng | Vägen till [!DNL Azure Blob] lagring. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `container.value` fält.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Azure Blob] [behållarnamn](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `container.value` fält för att läsa värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat behållarnamn för integreringen, till exempel `"path.value: myContainer"`och ange det här värdet till `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Sträng | Namnet på Azure Blob Storage-behållaren som ska användas för det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) målserver {#dlz-example}

Med den här målservern kan du exportera filer som innehåller plattformsdata till en [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) lagring.

Exemplet nedan visar ett exempel på en målserverkonfiguration för en [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Data Landing Zone] mål, ange detta till `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `path.value` fält.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Data Landing Zone] i användargränssnittet för Experience Platform anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallsialisera `path.value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "https://myaccount.blob.core.windows.net/"`och ange det här värdet till `NONE`. |
| `fileBasedDlzDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] målserver {#gcs-example}

Med den här målservern kan du exportera filer som innehåller plattformsdata till [!DNL Google Cloud Storage] konto.

Exemplet nedan visar ett exempel på en målserverkonfiguration för en [!DNL Google Cloud Storage] mål.

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
   }
}
```

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Google Cloud Storage] mål, ange detta till `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `bucket.value` fält.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Google Cloud Storage] hakparentesnamnet i användargränssnittet för Experience Platform, ange det här värdet som `PEBBLE_V1`. I det här fallet måste du mallsialisera `bucket.value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat kryckennamn för din integrering, till exempel `"bucket.value": "my-bucket"`och ange det här värdet till `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Sträng | Namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Sträng | *Obligatoriskt*. Ange det här värdet enligt den typ av värde som används i `path.value` fält.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Google Cloud Storage] bucket path in the Experience Platform UI, set this value to `PEBBLE_V1`. I det här fallet måste du mallsialisera `path.value` fält för att läsa ett värde från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "/path/to/my-bucket"`och ange det här värdet till `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Sträng | Sökvägen till [!DNL Google Cloud Storage] mapp som ska användas av det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafält](../destination-configuration/customer-data-fields.md) ifylld av användaren (som i exemplet ovan) eller ett hårdkodat värde, som `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vad en målserverspecifikation är och hur du kan konfigurera den.

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Mallspecifikationer](templating-specs.md)
* [Meddelandeformat](message-format.md)
* [Filformateringskonfiguration](file-formatting.md)
