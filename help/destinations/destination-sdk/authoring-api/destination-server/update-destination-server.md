---
description: Den här sidan innehåller exempel på API-anropet som används för att uppdatera en befintlig målserverkonfiguration via Adobe Experience Platform Destination SDK.
title: Uppdatera en målserverkonfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 8%

---


# Uppdatera en målserverkonfiguration

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att uppdatera en befintlig målserverkonfiguration med hjälp av `/authoring/destination-servers` API-slutpunkt.

>[!TIP]
>
>Alla uppdateringsåtgärder för produkterade/publika destinationer visas bara när du har använt [publicerings-API](../../publishing-api/create-publishing-request.md) och skicka in uppdateringen till Adobe för granskning.

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

## Uppdatera en målserverkonfiguration {#update}

Du kan uppdatera en [befintlig](create-destination-server.md) målserverkonfiguration genom att göra en `PUT` begäran till `/authoring/destination-servers` slutpunkt med uppdaterad nyttolast.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Så här hämtar du en befintlig målserverkonfiguration och dess motsvarande `{INSTANCE_ID}`, se artikeln om [hämta en målserverkonfiguration](retrieve-destination-server.md).

**API-format**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beskrivning |
| -------- | ----------- |
| `{INSTANCE_ID}` | ID:t för målserverkonfigurationen som du vill uppdatera. Så här hämtar du en befintlig målserverkonfiguration och dess motsvarande `{INSTANCE_ID}`, se [Hämta en målserverkonfiguration](retrieve-destination-server.md). |

Följande begäranden uppdaterar en befintlig målserverkonfiguration som konfigurerats med parametrarna i nyttolasten.

Välj varje flik nedan för att visa motsvarande nyttolast.

>[!BEGINTABS]

>[!TAB Realtid (direktuppspelning)]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Obligatoriskt.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i `value` fält nedan. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Använd `NONE` om ingen omformning behövs på Adobe-sidan, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Obligatoriskt.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |
| `httpTemplate.httpMethod` | Sträng | *Obligatoriskt.* Den metod som Adobe ska använda i anrop till servern. Alternativen är `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Sträng | *Obligatoriskt.* Använd `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Sträng | *Obligatoriskt.* Den här strängen är den teckenescape-konverterade version som transformerar data för plattformskunder till det format som tjänsten förväntar sig. <br> <ul><li> Mer information om hur du skriver mallen finns i [Använda mallavsnitt](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standard, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ett exempel på en enkel omformning finns i [Profilattribut](../../functionality/destination-server/message-format.md#attributes) omformning. </li></ul> |
| `httpTemplate.contentType` | Sträng | *Obligatoriskt.* Den innehållstyp som servern accepterar. Detta värde är mest sannolikt `application/json`. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB Amazon S3]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB SFTP]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB Azure Data Lake-lagring]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB Azure Blob Storage]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB DLZ (Data Landing Zone)]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!TAB Google Cloud-lagring]

+++Begäran

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Ett lyckat svar returnerar HTTP-status 200 med information om den uppdaterade målserverkonfigurationen.

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [fel i begäranhuvudet](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet kan du nu uppdatera en målserverkonfiguration via Destinationen SDK `/authoring/destination-servers` API-slutpunkt.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Skapa en målserverkonfiguration](create-destination-server.md)
* [Hämta en målserverkonfiguration](retrieve-destination-server.md)
* [Uppdatera en målserverkonfiguration](update-destination-server.md)