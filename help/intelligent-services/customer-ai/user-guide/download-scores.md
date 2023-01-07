---
keywords: Experience Platform;ladda ned poäng;kundnummer;populära ämnen;Exportera;exportera;kundnummer;kundpoäng
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Ladda ned bakgrundsmusik i kundens AI
description: Med kundens AI kan du hämta bakgrundsmusik i filformatet Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Ladda ned poäng i Customer AI

Det här dokumentet är en guide för nedladdning av poäng för kundens AI.

## Komma igång

Med kundens AI kan du hämta bakgrundsmusik i filformatet Parquet. Den här självstudiekursen kräver att du har läst och slutfört nedladdningen av AI-poäng för kunder i [komma igång](../getting-started.md) guide.

För att få tillgång till poäng för kunds-AI måste du dessutom ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [Konfigurera en AI-instans för kund](./configure.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

För närvarande finns det två sätt att hämta kundens AI-poäng:

1. Om du vill ladda ned poängen på individnivå och/eller inte har kundprofilen i realtid aktiverad börjar du med att navigera till [hitta ditt datauppsättnings-ID](#dataset-id).
2. Om du har en profil aktiverad och vill hämta segment som du har konfigurerat med hjälp av kundens AI går du till [ladda ned ett segment som konfigurerats med kundens AI](#segment).

## Hitta ditt datauppsättnings-ID {#dataset-id}

Klicka på *Fler åtgärder* i den övre högra navigeringen och välj **[!UICONTROL Access scores]**.

![fler åtgärder](../images/insights/more-actions.png)

En ny dialogruta visas med en länk till dokumentationen för nedladdning av bakgrundsmusik och datauppsättnings-ID:t för den aktuella instansen. Kopiera datauppsättnings-ID:t till Urklipp och fortsätt till nästa steg.

![Datauppsättnings-ID](../images/download-scores/access-scores.png)

## Hämta ditt batch-ID {#retrieve-your-batch-id}

Om du använder ditt datauppsättnings-ID från föregående steg måste du ringa ett anrop till katalog-API:t för att hämta ett batch-ID. Ytterligare frågeparametrar används för detta API-anrop för att returnera den senaste lyckade gruppen i stället för en lista med batchar som tillhör din organisation. Om du vill returnera ytterligare batchar ökar du talet för parametern limit query till det önskade belopp som du vill returnera. Mer information om vilka typer av frågeparametrar som finns finns finns i guiden på [filtrera katalogdata med frågeparametrar](../../../catalog/api/filter-data.md).

**API-format**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | Det datauppsättnings-ID som är tillgängligt i dialogrutan Åtkomstpoäng. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett batch-ID-objekt. I det här exemplet är nyckelvärdet för det returnerade objektet batch-ID `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopiera ditt batch-ID till nästa API-anrop.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Hämta nästa API-anrop med ditt batch-ID {#retrieve-the-next-api-call-with-your-batch-id}

När du har ditt batch-ID kan du göra en ny GET-förfrågan till `/batches`. Begäran returnerar en länk som används som nästa API-begäran.

**API-format**

```http
GET batches/{BATCH_ID}/files
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{BATCH_ID}` | Det batch-ID som hämtades i föregående steg [hämta ditt batch-ID](#retrieve-your-batch-id). |

**Begäran**

Använd ditt eget batch-ID och gör följande begäran.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller en `_links` -objekt. I `_links` objektet är ett `href` med ett nytt API-anrop som värde. Kopiera det här värdet för att fortsätta till nästa steg.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Hämta filer {#retrieving-your-files}

Använda `href` om du anger värdet som du fick i föregående steg som ett API-anrop, gör en ny GET-förfrågan för att hämta din filkatalog.

**API-format**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href` värde från [föregående steg](#retrieve-the-next-api-call-with-your-batch-id). Det finns även i `data` array under objekttypen `dataSetFileId`. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller en datamatris som kan ha en enda post eller en lista med filer som tillhör den katalogen. Exemplet nedan innehåller en lista med filer och har komprimerats för läsbarhet. I det här fallet måste du följa URL:en för varje fil för att kunna komma åt filen.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `_links.self.href` | Den URL för GET-begäran som används för att hämta en fil i din katalog. |


Kopiera `href` värde för alla filobjekt i `data` och gå sedan vidare till nästa steg.

## Hämta fildata

Om du vill hämta fildata skickar du en GET till `"href"` värde som du kopierade i föregående steg [hämta filer](#retrieving-your-files).

>[!NOTE]
>
>Om du gör den här begäran direkt i kommandoraden kanske du uppmanas att lägga till en utdatafil efter rubrikerna i din begäran. I följande exempel på begäran används `--output {FILENAME.FILETYPE}`.

**API-format**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href` värde från [föregående steg](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Filens namn. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Se till att du är i rätt katalog eller mapp som du vill att filen ska sparas i innan du skickar GETEN.

**Svar**

Svaret hämtar filen som du begärde i din aktuella katalog. I det här exemplet är filnamnet&quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Hämta ett segment som konfigurerats med kundens AI {#segment}

Ett annat sätt att ladda ned poängdata är att exportera målgruppen till en datauppsättning. När ett segmenteringsjobb har slutförts (värdet på `status` -attributet är &quot;SUCCEEDED&quot;), kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras. Mer information om segmentering finns på [segmenteringsöversikt](../../../segmentation/home.md).

>[!IMPORTANT]
>
>För att den här exportmetoden ska kunna användas måste kundprofilen i realtid aktiveras för datauppsättningen.

The [exportera ett segment](../../../segmentation/tutorials/evaluate-a-segment.md) i segmentutvärderingshandboken beskriver de steg som krävs för att exportera en målgruppsdatauppsättning. Stödlinjen innehåller konturer och exempel på följande:

- **Skapa en måldatauppsättning:** Skapa datauppsättningen för målgruppsmedlemmar.
- **Generera målgruppsprofiler i datauppsättningen:** Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- **Övervaka exportförlopp:** Kontrollera exportförloppet.
- **Läs målgruppsdata:** Hämta de resulterande enskilda XDM-profilerna som representerar medlemmarna i din publik.

## Nästa steg

I det här dokumentet beskrivs stegen som krävs för att hämta AI-poäng för kunder. Du kan nu fortsätta att bläddra bland de andra [Intelligenta tjänster](../../home.md) och guider som erbjuds.
