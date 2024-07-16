---
description: Den här sidan innehåller exempel på API-anropet som används för att skapa en målserver via Adobe Experience Platform Destination SDK.
title: Skapa en målserverkonfiguration
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 1%

---

# Skapa en målserverkonfiguration

Att skapa en målserver är det första steget när du ska skapa ett eget mål med Destination SDK. Målservern innehåller konfigurationsalternativ för specifikationerna [server](../../functionality/destination-server/server-specs.md) och [mallating](../../functionality/destination-server/templating-specs.md), [message format](../../functionality/destination-server/message-format.md) och [file formatting](../../functionality/destination-server/file-formatting.md) (för filbaserade mål).

Den här sidan innehåller exempel på API-begäran och nyttolast som du kan använda för att skapa en egen målserver med API-slutpunkten `/authoring/destination-servers`.

En detaljerad beskrivning av de funktioner som du kan konfigurera via den här slutpunkten finns i följande artiklar:

* [Serverspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Mallspecifikationer för mål som skapats med Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Meddelandeformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Filformateringskonfiguration](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alla parameternamn och värden som stöds av Destinationen SDK är **skiftlägeskänsliga**. Undvik skiftlägeskänslighetsfel genom att använda parameternamn och värden exakt som de visas i dokumentationen.

## Komma igång med API-åtgärder för målserver {#get-started}

Innan du fortsätter bör du läsa igenom [kom igång-guiden](../../getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive hur du får nödvändig behörighet för målredigering och nödvändiga rubriker.

## Skapa en målserverkonfiguration {#create}

Du kan skapa en ny målserverkonfiguration genom att göra en `POST`-begäran till `/authoring/destination-servers`-slutpunkten.

>[!TIP]
>
>**API-slutpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API-format**

```http
POST /authoring/destination-servers
```

Beroende på vilken måltyp du skapar måste du konfigurera en något annorlunda typ av målserver.

### Skapa statiska målservrar för schema {#static-destination-servers}

Se exempel på målservrar för mål som använder [statiska scheman](../../functionality/destination-configuration/schema-configuration.md#attributes-schema) på flikarna nedan.

Exempelnyttolasterna nedan innehåller alla parametrar som stöds av varje målservertyp. Du behöver inte inkludera alla parametrar i din begäran. Nyttolasten kan anpassas efter dina behov.

Välj varje flik nedan för att visa motsvarande API-begäranden.

>[!BEGINTABS]

>[!TAB Realtid (direktuppspelning)]

**Skapa en målserver för realtidsdirektuppspelning**

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
| `name` | Sträng | *Krävs.* Representerar ett eget namn för servern, som bara visas för Adobe. Detta namn är inte synligt för partners eller kunder. Exempel `Moviestar destination server`. |
| `destinationServerType` | Sträng | *Krävs.* Ange som `URL_BASED` för mål för realtidsströmning. |
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Krävs.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i fältet `value` nedan. Använd det här alternativet om du har en slutpunkt som `https://api.moviestar.com/data/{{customerData.region}}/items`, där `region`-delen kan skilja sig åt mellan kunder. I det här fallet måste du även konfigurera `region` som ett [kunddatafält](../../functionality/destination-configuration/customer-data-fields.md) i [målkonfigurationen] (../destination-configuration/create-destination-configuration.md). </li><li> Använd `NONE` om ingen omformning behövs på Adobe, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Krävs.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till. |
| `httpTemplate.httpMethod` | Sträng | *Krävs.* Den metod som Adobe ska använda i anrop till servern. Alternativen är `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Sträng | *Krävs.* Den här strängen är den teckenescape-version som omformar data för plattformskunder till det format som tjänsten förväntar sig. <br> <ul><li> Mer information om hur du skriver mallen finns i avsnittet [Använda mall](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standarden, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ett exempel på en enkel omformning finns i omformningen [Profilattribut](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Sträng | *Krävs.* Innehållstypen som servern accepterar. Det här värdet är troligen `application/json`. |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Amazon S3]

**Skapa en Amazon S3-målserver**

Du måste skapa en [!DNL Amazon S3]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL Amazon S3]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. För [!DNL Amazon S3] anger du det här till `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Sträng | Namnet på den [!DNL Amazon S3]-bucket som ska användas av det här målet. |
| `fileBasedS3Destination.path.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB SFTP]

**Skapa en [!DNL SFTP] målserver**

Du måste skapa en [!DNL SFTP]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL SFTP]-mål.

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
   "fileBasedSFTPDestination":{
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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_SFTP` för [!DNL SFTP] mål. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Sträng | Mållagringens rotkatalog. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Sträng | Mållagringens värdnamn. |
| `port` | Heltal | SFTP-filserverporten. |
| `encryptionMode` | Sträng | Anger om filkryptering ska användas. Värden som stöds: <ul><li>PGP</li><li>Ingen</li></ul> |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Azure Data Lake Storage]

**Skapa en [!DNL Azure Data Lake Storage] målserver**

Du måste skapa en [!DNL Azure Data Lake Storage]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL Azure Data Lake Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_ADLS_GEN2` för [!DNL Azure Data Lake Storage] mål. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Azure Blob Storage]

**Skapa en [!DNL Azure Blob Storage] målserver**

Du måste skapa en [!DNL Azure Blob Storage]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL Azure Blob Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_AZURE_BLOB` för [!DNL Azure Blob Storage] mål. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Sträng | Namnet på behållaren [!DNL Azure Blob Storage] som ska användas av det här målet. |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB DLZ (Data Landing Zone)]

**Skapa en [!DNL Data Landing Zone (DLZ)] målserver**

Du måste skapa en [!DNL Data Landing Zone (DLZ)]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL Data Landing Zone (DLZ)]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_DLZ` för [!DNL Data Landing Zone] mål. |
| `fileBasedDlzDestination.path.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!TAB Google Cloud-lagring]

**Skapa en [!DNL Google Cloud Storage] målserver**

Du måste skapa en [!DNL Google Cloud Storage]-målserver som liknar den som visas nedan när du konfigurerar ett filbaserat [!DNL Google Cloud Storage]-mål.

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
| `destinationServerType` | Sträng | Ange det här värdet enligt målplattformen. Ange detta till `FILE_BASED_GOOGLE_CLOUD` för [!DNL Google Cloud Storage] mål. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Sträng | Namnet på den [!DNL Google Cloud Storage]-bucket som ska användas av det här målet. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Sträng | Sökvägen till målmappen som ska vara värd för de exporterade filerna. |
| `fileConfigurations` | N/A | Mer information om hur du konfigurerar de här inställningarna finns i [filformateringskonfiguration](../../functionality/destination-server/file-formatting.md). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!ENDTABS]

### Skapa dynamiska målservrar för schema {#dynamic-schema-servers}

Med dynamiska scheman kan du dynamiskt hämta de målattribut som stöds och generera scheman baserat på ditt eget API. Du måste konfigurera en målserver för dynamiska scheman innan du kan konfigurera schemat.

På fliken nedan finns ett exempel på en målserver för mål som använder [dynamiska scheman](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration).

Nedan finns exempelnyttolasten med alla parametrar som krävs för en dynamisk schemaserver.

>[!BEGINTABS]

>[!TAB Dynamisk schemaserver]

**Skapa en dynamisk schemaserver**

Du måste skapa en dynamisk schemaserver som liknar den som visas nedan när du konfigurerar ett mål som hämtar sitt profilschema från din egen API-slutpunkt. I motsats till ett statiskt schema använder inte ett dynamiskt schema en `profileFields`-matris. I stället använder dynamiska scheman en dynamisk schemaserver som ansluter till din egen API från den plats där schemakonfigurationen hämtas.

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
| `name` | Sträng | *Krävs.* Representerar ett eget namn på din dynamiska schemaserver, som bara är synligt för Adobe. |
| `destinationServerType` | Sträng | *Krävs.* har angetts till `URL_BASED` för dynamiska schemaservrar. |
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Krävs.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i fältet `value` nedan. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Använd `NONE` om ingen omformning behövs på Adobe, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Krävs.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till och hämta schemafälten som ska fyllas i som målfält i mappningssteget i aktiveringsarbetsflödet. |
| `httpTemplate.httpMethod` | Sträng | *Krävs.* Den metod som Adobe ska använda i anrop till servern. Använd `GET` för dynamiska schemaservrar. |
| `responseFields.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `responseFields.value` | Sträng | *Krävs.* Den här strängen är den omformningsmall för tecken som escape-konverterar svar från partner-API:t till det partnerschema som ska visas i plattformsgränssnittet. <br> <ul><li> Mer information om hur du skriver mallen finns i avsnittet [Använda mall](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standarden, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ett exempel på en enkel omformning finns i omformningen [Profilattribut](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++


>[!ENDTABS]


### Skapa dynamiska målservrar för listrutor {#dynamic-dropdown-servers}

Använd [dynamiska listrutor](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) för att dynamiskt hämta och fylla i kunddatafält i listrutor baserat på ditt eget API. Du kan till exempel hämta en lista över befintliga användarkonton som du vill använda för en målanslutning.

Du måste konfigurera en målserver för dynamiska listrutor innan du kan konfigurera det dynamiska listrutan för kunddatafältet.

På fliken nedan finns ett exempel på en målserver som används för att dynamiskt hämta de värden som ska visas i en listruteväljare från ett API.

Nedan finns exempelnyttolasten med alla parametrar som krävs för en dynamisk schemaserver.

>[!BEGINTABS]

>[!TAB Dynamisk listruteserver]

**Skapa en dynamisk listruteserver**

Du måste skapa en dynamisk nedrullningsbar server som liknar den som visas nedan när du konfigurerar ett mål som hämtar värdena för ett nedrullningsbart kunddatafält från din egen API-slutpunkt.

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
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parameter | Typ | Beskrivning |
| -------- | ----------- | ----------- |
| `name` | Sträng | *Krävs.* Representerar ett eget namn på den dynamiska nedrullningsbara servern, som bara är synlig för Adobe. |
| `destinationServerType` | Sträng | *Krävs.* anges till `URL_BASED` för dynamiska listruteservrar. |
| `urlBasedDestination.url.templatingStrategy` | Sträng | *Krävs.* <ul><li>Använd `PEBBLE_V1` om Adobe behöver omvandla URL:en i fältet `value` nedan. Använd det här alternativet om du har en slutpunkt som: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Använd `NONE` om ingen omformning behövs på Adobe, till exempel om du har en slutpunkt som: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Sträng | *Krävs.* Fyll i adressen till API-slutpunkten som Experience Platform ska ansluta till och hämta listrutans värden. |
| `httpTemplate.httpMethod` | Sträng | *Krävs.* Den metod som Adobe ska använda i anrop till servern. Använd `GET` för dynamiska listruteservrar. |
| `httpTemplate.headers` | Objekt | *Option.l* Inkludera alla huvuden som krävs för att ansluta till den dynamiska listruteservern. |
| `responseFields.templatingStrategy` | Sträng | *Krävs.* Använd `PEBBLE_V1`. |
| `responseFields.value` | Sträng | *Krävs.* Den här strängen är den omformningsmall för tecken som escape-konverterar svar från ditt API till värden som ska visas i plattformsgränssnittet. <br> <ul><li> Mer information om hur du skriver mallen finns i avsnittet [Använda mall](../../functionality/destination-server/message-format.md#using-templating). </li><li> Mer information om teckenigenkänning finns i [RFC JSON-standarden, avsnitt sju](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++svar

Ett lyckat svar returnerar HTTP-status 200 med information om den nya målserverkonfigurationen.

+++

>[!ENDTABS]

## API-felhantering {#error-handling}

Destination SDK-API-slutpunkter följer de allmänna felmeddelandeprinciperna för Experience Platform API. Se [API-statuskoder](../../../../landing/troubleshooting.md#api-status-codes) och [begäranrubrikfel](../../../../landing/troubleshooting.md#request-header-errors) i felsökningsguiden för plattformen.

## Nästa steg {#next-steps}

När du har läst det här dokumentet vet du nu hur du skapar en ny målserver via API-slutpunkten för Destinationen SDK `/authoring/destination-servers`.

Mer information om vad du kan göra med den här slutpunkten finns i följande artiklar:

* [Hämta en målserverkonfiguration](retrieve-destination-server.md)
* [Uppdatera en målserverkonfiguration](update-destination-server.md)
* [Ta bort en målserverkonfiguration](delete-destination-server.md)

Mer information om var den här slutpunkten passar in i målredigeringsprocessen finns i följande artiklar:

* [Använd Destination SDK för att konfigurera ett direktuppspelningsmål](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Använd Destination SDK för att konfigurera ett filbaserat mål](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
