---
description: Lär dig hur du konfigurerar filformateringsalternativ för filbaserade mål som skapats med Adobe Experience Platform Destination SDK via slutpunkten "/destination-servers".
title: Filformateringskonfiguration
exl-id: 98fec559-9073-4517-a10e-34c2caf292d5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 2%

---

# Filformateringskonfiguration

Destinationen SDK har stöd för en flexibel uppsättning funktioner som du kan konfigurera efter dina integrationsbehov. Bland dessa funktioner finns stöd för [!DNL CSV] filformatering.

När du skapar filbaserade mål via Destination SDK kan du definiera hur de exporterade CSV-filerna ska formateras. Du kan anpassa många formateringsalternativ, till exempel, men inte begränsat till:

* Anger om CSV-filen ska innehålla en rubrik,
* Vilket tecken som ska användas för att citera värden,
* Hur tomma värden ska se ut.

Beroende på målkonfigurationen visas vissa alternativ i användargränssnittet när du ansluter till ett filbaserat mål. Du kan se hur dessa alternativ ser ut i dialogrutan [filformateringsalternativ för filbaserade mål](../../../ui/batch-destinations-file-formatting-options.md) dokumentation.


Filformateringsinställningarna ingår i målserverkonfigurationen för filbaserade mål.

Mer information om var den här komponenten passar in i en integrering som skapas med Destination SDK finns i diagrammet i [konfigurationsalternativ](../configuration-options.md) eller se guiden om hur du [använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Du kan konfigurera filformateringsalternativen via `/authoring/destination-servers` slutpunkt. På följande API-referenssidor finns detaljerade API-anropsexempel där du kan konfigurera komponenterna som visas på den här sidan.

* [Skapa en målserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Uppdatera en målserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

På den här sidan beskrivs alla filformatsinställningar som stöds för exporterade filer `CSV` filer.

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Integrationstyper som stöds {#supported-integration-types}

Se tabellen nedan för mer ingående information om vilka typer av integreringar som stöder de funktioner som beskrivs på den här sidan.

| Integrationstyp | Stöder funktioner |
|---|---|
| Integrering i realtid (direktuppspelning) | Nej |
| Filbaserade (batch) integreringar | Ja |

## parametrar som stöds {#supported-parameters}

Du kan ändra flera egenskaper för de exporterade filerna så att de matchar kraven i mottagningssystemet för målfilen, för att optimera läsningen och tolkningen av de filer som tas emot från Experience Platform.

>[!NOTE]
>
>CSV-alternativ stöds bara när CSV-filer exporteras. The `fileConfigurations` -avsnittet är inte obligatoriskt när du konfigurerar en ny målserver. Om du inte skickar några värden i API-anropet för CSV-alternativen är standardvärdena från [referenstabell längre ned](#file-formatting-reference-and-example) kommer att användas.


## CSV-alternativ där användarna inte kan välja konfigurationsalternativ {#file-configuration-templating-none}

I konfigurationsexemplet nedan är alla CSV-alternativ fördefinierade. De exportinställningar som definieras i var och en av `csvOptions` parametrar är slutgiltiga och användarna kan inte ändra dem.

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
            }
        },
        "maxFileRowCount":5000000,
        "includeFileManifest": {
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{ customerData.includeFileManifest }}"
      }
    }
```

## CSV-alternativ där användarna kan välja konfigurationsalternativ {#file-configuration-templating-pebble}

I konfigurationsexemplet nedan är inget av CSV-alternativen fördefinierat. The `value` i varje `csvOptions` parametrarna har konfigurerats i ett motsvarande kunddatafält via `/destinations` slutpunkt (till exempel [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) för `quote` filformateringsalternativ) och användare kan använda användargränssnittet i Experience Platform för att välja mellan de olika alternativ som du konfigurerar i motsvarande kunddatafält. Du kan se hur dessa alternativ ser ut i dialogrutan [filformateringsalternativ för filbaserade mål](../../../ui/batch-destinations-file-formatting-options.md) dokumentation.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      },
      "maxFileRowCount":5000000,
      "includeFileManifest": {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{ customerData.includeFileManifest }}"
      }
   }
}
```

## Fullständig referens och exempel för de filformateringsalternativ som stöds {#file-formatting-reference-and-example}

>[!TIP]
>
>CSV-filformateringsalternativen som beskrivs nedan beskrivs även i [Apache Spark-guide för CSV-filer](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Beskrivningarna nedan är hämtade från Apache Spark-guiden.

Nedan visas en fullständig referens över alla tillgängliga filformateringsalternativ i Destination SDK, tillsammans med utdataexempel för varje alternativ.

| Fält | Obligatoriskt/valfritt | Beskrivning | Standardvärde | Exempel på utdata 1 | Exempel på utdata 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obligatoriskt | För varje filformateringsalternativ som du konfigurerar måste du lägga till parametern `templatingStrategy`, som kan ha två värden: <br><ul><li>`NONE`: använd det här värdet om du inte planerar att låta användarna välja mellan olika värden för en konfiguration. Se [den här konfigurationen](#file-configuration-templating-none) till exempel där filformateringsalternativen är fasta.</li><li>`PEBBLE_V1`: använd det här värdet om du vill att användarna ska kunna välja mellan olika värden för en konfiguration. I det här fallet måste du även skapa ett motsvarande kunddatafält i `/destination` slutpunktskonfiguration för att visa de olika alternativen för användarna i användargränssnittet. Se [den här konfigurationen](#file-configuration-templating-pebble) till exempel där användare kan välja mellan olika värden för filformateringsalternativ.</li></ul> | – | – | – |
| `compression.value` | Valfritt | Komprimeringskodek som ska användas när data sparas i en fil. Värden som stöds: `none`, `bzip2`, `gzip`, `lz4`och `snappy`. | `none` | – | – |
| `fileType.value` | Valfritt | Anger utdatafilens format. Värden som stöds: `csv`, `parquet`och `json`. | `csv` | – | – |
| `csvOptions.quote.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger ett enskilt tecken som används för att undvika citattecken där avgränsaren kan vara en del av värdet. | `null` | Exempel på standardvärde: `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | Exempel: `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om alla värden alltid ska omslutas av citattecken. Som standard är det bara escape-värden som innehåller ett citattecken. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger en avgränsare för varje fält och värde. Avgränsaren kan vara ett eller flera tecken. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Ställer in ett enskilt tecken som används för att undvika citattecken inuti ett redan citattecken. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om värden som innehåller citattecken alltid ska omslutas av citattecken. Standard är att undvika alla värden som innehåller ett citattecken. | `true` | – | – |
| `csvOptions.header.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om kolumnnamnen ska skrivas som den första raden i den exporterade filen. | `true` | – | – |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om inledande blanksteg ska trimmas från värden. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger om efterföljande blanksteg ska trimmas från värden. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängbeteckningen för ett null-värde. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger datumformatet. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängen som anger ett tidsstämpelformat. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | – | – |
| `csvOptions.charToEscapeQuoteEscaping.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Ställer in ett enda tecken som används för att kringgå citattecknet. | `\` när escape- och citattecknen är olika. `\0` när escape- och citattecknet är detsamma. | – | – |
| `csvOptions.emptyValue.value` | Valfritt | *Endast för`"fileType.value": "csv"`*. Anger strängbeteckningen för ett tomt värde. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | Valfritt | Anger det maximala antalet rader per exporterad fil, mellan 1 000 000 och 10 000 000 rader. | 5,000,000 |
| `includeFileManifest` | Valfritt | Aktiverar stöd för export av ett filmanifest tillsammans med filexporten. Manifestets JSON-fil innehåller information om exportplats, exportstorlek med mera. Manifestet har ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. | Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält: <ul><li>`flowRunId`: [dataflödeskörning](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.</li><li>`scheduledTime`: Tiden i UTC när filen exporterades. </li><li>`exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras. </li><li>`exportResults.name`: Namnet på den exporterade filen.</li><li>`size`: Storleken på den exporterade filen, i byte.</li></ul> |

{style="table-layout:auto"}

## Nästa steg {#next-steps}

När du har läst den här artikeln bör du få en bättre förståelse för hur filformatering fungerar i en målserverkonfiguration och hur du kan konfigurera den.

Mer information om andra målserverkomponenter finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](server-specs.md)
* [Mallspecifikationer](templating-specs.md)
* [Meddelandeformat](message-format.md)
