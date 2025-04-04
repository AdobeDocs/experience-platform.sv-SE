---
description: Lär dig hur du konfigurerar målserverspecifikationer i Adobe Experience Platform Destination SDK via slutpunkten "/authoring/destination-servers".
title: Serverspecifikationer för mål som skapats med Destination SDK
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 0%

---

# Serverspecifikationer för mål som skapats med Destination SDK

Målserverns specifikationer definierar vilken typ av målplattform som ska ta emot data från Adobe Experience Platform och kommunikationsparametrarna mellan Experience Platform och ditt mål. Till exempel:

* En [målserverspecifikation för direktuppspelning](#streaming-example) definierar HTTP-serverslutpunkten som tar emot HTTP-meddelanden från Experience Platform. Om du vill lära dig att konfigurera hur HTTP-anrop till slutpunkten formateras läser du sidan [Mallating specs](templating-specs.md) .
* En [Amazon S3](#s3-example)-målserverspecifikation definierar namnet på [!DNL S3]-bucket och sökvägen dit Experience Platform ska exportera filerna.
* En [SFTP](#sftp-example)-målserverspecifikation definierar värdnamnet, rotkatalogen, kommunikationsporten och krypteringstypen för SFTP-servern där Experience Platform ska exportera filerna.

Om du vill veta var den här komponenten passar in i en integrering som skapats med Destination SDK kan du läsa diagrammet i dokumentationen för [konfigurationsalternativ](../configuration-options.md) eller följande sidor med en översikt över målkonfigurationen:

* [Använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Du kan konfigurera målserverspecifikationerna via slutpunkten `/authoring/destination-servers`. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Uppdatera en målserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

På den här sidan visas alla målservertyper som stöds av Destination SDK, med alla deras konfigurationsparametrar. Ersätt parametervärdena med dina egna när du skapar målet.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destination SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Ja |
| Filbaserade (batch) integreringar | Ja |

När du [skapar](../../authoring-api/destination-server/create-destination-server.md) eller [uppdaterar](../../authoring-api/destination-server/update-destination-server.md) en målserver ska du använda någon av de servertypskonfigurationer som beskrivs på den här sidan. Beroende på dina integrationskrav ska du se till att ersätta exempelparametervärdena från de här exemplen med dina egna.

## Hårdkodade jämfört med mallsidesfält {#templatized-fields}

När du skapar en målserver med Destination SDK kan du definiera parametervärden för konfiguration antingen genom att hårdkoda dem i konfigurationen eller genom att använda mallfält. I mallbaserade fält kan du läsa användardefinierade värden från användargränssnittet i Experience Platform.

Målserverparametrar har två konfigurerbara fält. Dessa alternativ avgör om du använder hårdkodade eller mallsidiga värden.

| Parameter | Typ | Beskrivning |
|---|---|---|
| `templatingStrategy` | Sträng | *Krävs.* Definierar om det finns ett hårdkodat värde som tillhandahålls via fältet `value` eller ett användarkonfigurerbart värde i användargränssnittet. Värden som stöds: <ul><li>`NONE`: Använd det här värdet när du hårdkodar parametervärdet via parametern `value` (se nästa rad). Exempel:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Använd det här värdet när du vill att användarna ska ange ett parametervärde i användargränssnittet. Exempel: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Sträng | *Krävs*. Definierar parametervärdet. Värdetyper som stöds: <ul><li>**Hårdkodat värde**: Använd ett hårdkodat värde (till exempel `"value": "my-storage-bucket"`) om du inte behöver att användarna anger ett parametervärde i gränssnittet. När du hårdkodar ett värde ska `templatingStrategy` alltid anges till `NONE`.</li><li>**Mallat värde**: Använd ett mallbaserat värde (till exempel `"value": "{{customerData.bucket}}"`) när du vill att användarna ska ange ett parametervärde i användargränssnittet. När du använder mallsidiga värden ska `templatingStrategy` alltid anges till `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### När hårdkodade jämfört med mallsidesfält ska användas

Både hårdkodade och mallbaserade fält kan användas i Destination SDK, beroende på vilken typ av integrering du skapar.

**Ansluter till målet utan användarindata**

När användare [ansluter till ditt mål](../../../ui/connect-destination.md) i Experience Platform-gränssnittet kanske du vill hantera målanslutningsprocessen utan indata.

Det gör du genom att hårdkoda anslutningsparametrarna för målplattformen i serverspecifikationen. När du använder hårdkodade parametervärden i målserverkonfigurationen hanteras anslutningen mellan Adobe Experience Platform och målplattformen utan indata från användaren.

I exemplet nedan skapar en partner en Data Landing Zone-målserver med fältet `path.value` som hårdkodas.

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

Det innebär att användare som går igenom självstudiekursen [för målanslutning](../../../ui/connect-destination.md) inte kommer att se något [autentiseringssteg](../../../ui/connect-destination.md#authenticate). Autentiseringen hanteras i stället av Experience Platform, vilket visas i bilden nedan.

![Användargränssnittsbild som visar autentiseringsskärmen mellan Experience Platform och ett DLZ-mål.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Ansluter till målet med användarindata**

När anslutningen mellan Experience Platform och ditt mål ska upprättas efter en viss användarinmatning i Experience Platform-gränssnittet, till exempel val av en API-slutpunkt eller tillhandahållande av ett fältvärde, kan du använda mallfält i serverspecifikationen för att läsa användarinmatningen och ansluta till målplattformen.

I exemplet nedan skapar en partner en [realtidsintegrering (direktuppspelning)](#streaming-example) och fältet `url.value` använder den mallatiserade parametern `{{customerData.region}}` för att anpassa en del av API-slutpunkten baserat på användarindata.

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

Om du vill att användare ska kunna välja ett värde i användargränssnittet i Experience Platform måste parametern `region` också definieras i [målkonfigurationen](../../authoring-api/destination-configuration/create-destination-configuration.md) som ett kunddatafält, vilket visas nedan:

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

Detta innebär att användare som går igenom självstudiekursen [för målanslutning](../../../ui/connect-destination.md) måste välja en region innan de kan ansluta till målplattformen. När de ansluter till målet ersätts det mallbaserade fältet `{{customerData.region}}` med det värde som användaren har valt i användargränssnittet, vilket visas i bilden nedan.

![Användargränssnittsbild som visar målanslutningsskärmen med en regionväljare.](../../assets/functionality/destination-server/server-spec-template-region.png)

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
| `name` | Sträng | *Krävs.* Representerar ett eget namn på servern, som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel: `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Krävs.* Ange detta till `URL_BASED` för direktuppspelningsmål. |
| `templatingStrategy` | Sträng | *Krävs.* <ul><li>Använd `PEBBLE_V1` om du använder ett mallbaserat fält i stället för ett hårdkodat värde i fältet `value`. Använd det här alternativet om du har en slutpunkt som `https://api.moviestar.com/data/{{customerData.region}}/items`, där användarna måste välja slutpunktsområdet i Experience Platform-gränssnittet. </li><li> Använd `NONE` om det inte behövs någon mallad omvandling på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Sträng | *Krävs.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Om du vill exportera filer till en [!DNL Amazon S3]-bucket anger du den här till `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `bucket.value`.<ul><li>Om du vill att dina användare ska ange sina egna Bucket-namn i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat pytsnamn för integreringen, till exempel `"bucket.value":"MyBucket"`, ska du ange det här värdet som `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Sträng | Namnet på den [!DNL Amazon S3]-bucket som ska användas av det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `path.value`.<ul><li>Om du vill att dina användare ska ange sin egen sökväg i Experience Platform-gränssnittet anger du värdet `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `path.value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"bucket.value":"/path/to/MyBucket"`, anger du det här värdet till `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Sträng | Sökvägen till den [!DNL Amazon S3]-bucket som ska användas av det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] målserver {#sftp-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till lagringsservern [!DNL SFTP].

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Om du vill exportera filer till ett [!DNL SFTP]-mål anger du `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `rootDirectory.value`.<ul><li>Om du vill att dina användare ska ange sin egen rotkatalogsökväg i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `rootDirectory.value` för att läsa ett användartillhandahållet värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad rotkatalogsökväg för din integrering, till exempel `"rootDirectory.value":"Storage/MyDirectory"`, anger du det här värdet till `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Sträng | Sökvägen till den katalog som ska vara värd för de exporterade filerna. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `hostName.value`.<ul><li>Om du vill att dina användare ska ange sitt eget värdnamn i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `hostName.value` för att läsa ett användartillhandahållet värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat värdnamn för din integrering, till exempel `"hostName.value":"my.hostname.com"`, anger du det här värdet till `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Sträng | Värdnamnet för SFTP-servern. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"hostName.value":"my.hostname.com"`. |
| `port` | Heltal | SFTP-filserverporten. |
| `encryptionMode` | Sträng | Anger om filkryptering ska användas. Värden som stöds: <ul><li>PGP</li><li>Ingen</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) målserver {#adls-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till ditt [!DNL Azure Data Lake Storage]-konto.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett [!DNL Azure Data Lake Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_ADLS_GEN2` för [!DNL Azure Data Lake Storage] mål. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `path.value`.<ul><li>Om du vill att dina användare ska ange sin [!DNL ADLS]-mappsökväg i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `path.value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, anger du det här värdet till `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Sträng | Sökvägen till lagringsmappen [!DNL ADLS]. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] målserver {#blob-example}

Med den här målservern kan du exportera filer som innehåller Adobe Experience Platform-data till [!DNL Azure Blob Storage]-behållaren.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett [!DNL Azure Blob Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_AZURE_BLOB` för [!DNL Azure Blob Storage] mål. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `path.value`.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Azure Blob] [lagringskontots URI](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `path.value` för att kunna läsa värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "https://myaccount.blob.core.windows.net/"`, anger du det här värdet till `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Sträng | Sökvägen till ditt [!DNL Azure Blob]-lagringsutrymme. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `container.value`.<ul><li>Om du vill att dina användare ska ange sitt eget [!DNL Azure Blob] [behållarnamn](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `container.value` för att kunna läsa värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat behållarnamn för integreringen, till exempel `"path.value: myContainer"`, anger du det här värdet till `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Sträng | Namnet på Azure Blob Storage-behållaren som ska användas för det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) målserver {#dlz-example}

Med den här målservern kan du exportera filer som innehåller Experience Platform-data till ett [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md)-lagringsutrymme.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett [!DNL Data Landing Zone] ([!DNL DLZ])-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_DLZ` för [!DNL Data Landing Zone] mål. |
| `fileBasedDlzDestination.path.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `path.value`.<ul><li>Om du vill att dina användare ska ange sitt eget [!DNL Data Landing Zone]-konto i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `path.value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "https://myaccount.blob.core.windows.net/"`, anger du det här värdet till `NONE`. |
| `fileBasedDlzDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] målserver {#gcs-example}

Med den här målservern kan du exportera filer som innehåller Experience Platform-data till ditt [!DNL Google Cloud Storage]-konto.

Exemplet nedan visar ett exempel på en målserverkonfiguration för ett [!DNL Google Cloud Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_GOOGLE_CLOUD` för [!DNL Google Cloud Storage] mål. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `bucket.value`.<ul><li>Om du vill att dina användare ska ange sina egna [!DNL Google Cloud Storage]-bucket-namn i Experience Platform-gränssnittet anger du det här värdet som `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `bucket.value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder ett hårdkodat pytsnamn för integreringen, till exempel `"bucket.value": "my-bucket"`, ska du ange det här värdet som `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Sträng | Namnet på den [!DNL Google Cloud Storage]-bucket som ska användas av det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Sträng | *Krävs*. Ange det här värdet enligt den typ av värde som används i fältet `path.value`.<ul><li>Om du vill att dina användare ska ange sin egen [!DNL Google Cloud Storage]-bucket-sökväg i Experience Platform-gränssnittet anger du det här värdet till `PEBBLE_V1`. I det här fallet måste du mallatisera fältet `path.value` för att läsa ett värde från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren. Det här användningsexemplet visas i exemplet ovan.</li><li>Om du använder en hårdkodad sökväg för din integrering, till exempel `"path.value": "/path/to/my-bucket"`, anger du det här värdet till `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Sträng | Sökvägen till mappen [!DNL Google Cloud Storage] som ska användas av det här målet. Detta kan antingen vara ett mallbaserat fält som läser värdet från [kunddatafälten](../destination-configuration/customer-data-fields.md) som fyllts i av användaren (som visas i exemplet ovan) eller ett hårdkodat värde, som `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för vad en målserverspecifikation är och hur du kan konfigurera den.

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Mallspecifikationer](templating-specs.md)
* [Meddelandeformat](message-format.md)
* [Filformateringskonfiguration](file-formatting.md)
