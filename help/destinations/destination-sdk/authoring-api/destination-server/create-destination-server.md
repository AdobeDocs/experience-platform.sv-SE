---
description: Den här sidan innehåller exempel på API-anropet som används för att skapa en målserver via Adobe Experience Platform Destination SDK.
title: Skapa en målserverkonfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 6%

---


# Skapa en målserverkonfiguration

Att skapa en målserver är det första steget när du ska skapa ett eget mål med Destination SDK. Målservern innehåller konfigurationsalternativ för [server](../../functionality/destination-server/server-specs.md) och [mallsätta](../../functionality/destination-server/templating-specs.md) specifikationer, [meddelandeformat](../../functionality/destination-server/message-format.md)och [filformatering](../../functionality/destination-server/file-formatting.md) alternativ (för filbaserade mål).

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en egen målserver med hjälp av `/authoring/destination-servers` API-slutpunkt.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Mallspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Meddelandeformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Filformateringskonfiguration](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänslig**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målserver {#get-started}

Läs igenom [komma igång-guide](../../getting-started.md) för viktig information som du behöver känna till för att kunna anropa API:t, inklusive hur du får nödvändig behörighet för målredigering och obligatoriska huvuden.

## Skapa en målserverkonfiguration {#create}

Du kan skapa en ny målserverkonfiguration genom att skapa en `POST` begäran till `/authoring/destination-servers` slutpunkt.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API-format**

```http
POST /authoring/destination-servers
```

Beroende på vilken måltyp du skapar måste du konfigurera en något annorlunda typ av målserver. Se exempel på målservrar för varje måltyp som stöds i Destinationen SDK i flikarna nedan.

Exempelnyttolasterna nedan innehåller alla parametrar som stöds av varje målservertyp. Du behöver inte inkludera alla parametrar i din begäran. Nyttolasten kan anpassas efter dina behov.

Välj varje flik nedan för att visa motsvarande API-begäranden.

>[!BEGINTABS]

>[!TAB Realtid (direktuppspelning)]

**Skapa en målserver för realtid (direktuppspelning)**

Du måste skapa en målserver för realtid (direktuppspelning) som liknar den som visas nedan när du konfigurerar en API-baserad integrering för realtid (direktuppspelning).

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `name` | Sträng | *Obligatoriskt.* Representerar ett eget namn på servern som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Obligatoriskt.* Ange till `URL_BASED` för mål för realtidsströmning. |
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i `value` fält nedan. Använd det här alternativet om du har en slutpunkt som `https://api.moviestar.com/data/{{customerData.region}}/items`, där `region` kan skilja sig mellan kunderna. I det här fallet måste du även konfigurera `region` som [kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) i [målkonfiguration](../destination-configuration/create-destination-configuration.md. </li><li> Använd `NONE` om ingen omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |
| `httpTemplate.httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. Alternativen är `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Sträng | *Obligatoriskt.* Den här strängen är den teckenescape-konverterade version som transformerar data för plattformskunder till det format som tjänsten förväntar sig. <br> <ul><li> Mer information om hur du skriver mallen finns i [Använda mallavsnitt](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standard, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ett exempel på en enkel omformning finns i [Profilattribut](../../functionality/destination-server/message-format.md#attributes) omformning. </li></ul> |
| `httpTemplate.contentType` | Sträng | *Obligatoriskt.* Den innehållstyp som servern accepterar. Detta värde är mest sannolikt `application/json`. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Amazon S3]

**Skapa en Amazon S3-målserver**

Du måste skapa en [!DNL Amazon S3] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL Amazon S3] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Amazon S3], ange detta till `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Sträng | Namnet på [!DNL Amazon S3] bucket som ska användas för detta mål. |
| `fileBasedS3Destination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB SFTP]

**Skapa en [!DNL SFTP] målserver**

Du måste skapa en [!DNL SFTP] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL SFTP] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
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
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Azure Data Lake-lagring]

**Skapa en [!DNL Azure Data Lake Storage] målserver**

Du måste skapa en [!DNL Azure Data Lake Storage] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL Azure Data Lake Storage] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Data Lake Storage] mål, ange detta till `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Azure Blob Storage]

**Skapa en [!DNL Azure Blob Storage] målserver**

Du måste skapa en [!DNL Azure Blob Storage] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL Azure Blob Storage] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Azure Blob Storage] mål, ange detta till `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Sträng | Namnet på [!DNL Azure Blob Storage] behållare som ska användas av det här målet. |
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB DLZ (Data Landing Zone)]

**Skapa en [!DNL Data Landing Zone (DLZ)] målserver**

Du måste skapa en [!DNL Data Landing Zone (DLZ)] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL Data Landing Zone (DLZ)] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Data Landing Zone] mål, ange detta till `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Google Cloud-lagring]

**Skapa en [!DNL Google Cloud Storage] målserver**

Du måste skapa en [!DNL Google Cloud Storage] målserver som liknar den som visas nedan när du konfigurerar en filbaserad [!DNL Google Cloud Storage] mål.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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

| Parameter | Typ | Beskrivning |
|---|---|---|
| `name` | Sträng | Namnet på målanslutningen. |
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Google Cloud Storage] mål, ange detta till `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Sträng | Namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | Ej tillämpligt | Se [filformatskonfiguration](../../functionality/destination-server/file-formatting.md) om du vill ha mer information om hur du konfigurerar de här inställningarna. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Dynamisk schemaserver]

**Skapa en dynamisk schemaserver**

Du måste skapa en dynamisk schemaserver som liknar den som visas nedan när du konfigurerar ett mål som hämtar sitt profilschema från din egen API-slutpunkt. I motsats till ett statiskt schema använder ett dynamiskt schema inte ett `profileFields` array. I stället använder dynamiska scheman en dynamisk schemaserver som ansluter till din egen API från den plats där schemakonfigurationen hämtas.

+++Begäran

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `name` | Sträng | *Obligatoriskt.* Representerar ett eget namn på den dynamiska schemaservern som bara visas för Adobe. |
| `destinationServerType` | Sträng | *Obligatoriskt.* Ange till `URL_BASED` för dynamiska schemaservrar. |
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i `value` fält nedan. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Använd `NONE` om ingen omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till och hämta schemafälten för att fylla i som målfält i mappningssteget i aktiveringsarbetsflödet. |
| `httpTemplate.httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. För dynamiska schemaservrar använder du `GET`. |
| `responseFields.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `responseFields.value` | Sträng | *Obligatoriskt.* Den här strängen är den omformningsmall för tecken som escape-konverterar svar från partner-API:t till det partnerschema som visas i plattformens användargränssnitt. <br> <ul><li> Mer information om hur du skriver mallen finns i [Använda mallavsnitt](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standard, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ett exempel på en enkel omformning finns i [Profilattribut](../../functionality/destination-server/message-format.md#attributes) omformning. </li></ul> |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du skapar en ny målserver via Destinationen SDK `/authoring/destination-servers` API-slutpunkt.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Hämta en målserverkonfiguration](retrieve-destination-server.md)
* [Uppdatera en målserverkonfiguration](update-destination-server.md)
* [Ta bort en målserverkonfiguration](delete-destination-server.md)

Mer information om var den här slutpunkten passar in i målredigeringsprocessen finns i följande artiklar:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)