---
keywords: Experience Platform;download scores;customer ai;popular topics;Export;export
solution: Experience Platform
title: Ladda ned bakgrundsmusik i kundens AI
topic: Downloading scores
description: Med Customer AI kan du hämta poäng i parquet-filformat.
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# Ladda ned bakgrundsmusik i kundens AI

Det här dokumentet är en guide för nedladdning av poäng för kundens AI.

## Komma igång

Med Customer AI kan du hämta poäng i parquet-filformat. Den här självstudien kräver att du har läst och slutfört nedladdningen av AI-poängen för kunder i guiden [Komma igång](../getting-started.md) .

För att få tillgång till poäng för kunds-AI måste du dessutom ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [Konfigurera en AI-instans](./configure.md)för kunder. Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

För närvarande finns det två sätt att hämta kundens AI-poäng:

1. Om du vill hämta poängen på individuell nivå och/eller inte har kundprofilen i realtid aktiverad börjar du med att [hitta ditt datauppsättnings-ID](#dataset-id).
2. Om du har en profil aktiverad och vill hämta segment som du har konfigurerat med hjälp av kundens AI, navigerar du till [hämtningen av ett segment som har konfigurerats med kundens AI](#segment).

## Hitta ditt datauppsättnings-ID {#dataset-id}

Klicka på listrutan *Fler åtgärder* i den övre högra navigeringsfältet i tjänstinstansen och välj sedan **[!UICONTROL Access scores]**.

![fler åtgärder](../images/insights/more-actions.png)

En ny dialogruta visas med en länk till dokumentationen för nedladdning av bakgrundsmusik och datauppsättnings-ID:t för den aktuella instansen. Kopiera datauppsättnings-ID:t till Urklipp och fortsätt till nästa steg.

![Datauppsättnings-ID](../images/download-scores/access-scores.png)

## Hämta ditt batch-ID {#retrieve-your-batch-id}

Om du använder ditt datauppsättnings-ID från föregående steg måste du ringa ett anrop till katalog-API:t för att hämta ett batch-ID. Ytterligare frågeparametrar används för detta API-anrop för att returnera den senaste lyckade gruppen i stället för en lista med batchar som tillhör din organisation. Om du vill returnera ytterligare batchar ökar du talet för parametern limit query till det önskade belopp som du vill returnera. Mer information om vilka typer av frågeparametrar som finns tillgängliga finns i guiden om [filtrering av katalogdata med hjälp av frågeparametrar](../../../catalog/api/filter-data.md).

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `{BATCH_ID}` | Det batch-ID som hämtades i föregående steg [hämtar ditt batch-ID](#retrieve-your-batch-id). |

**Begäran**

Använd ditt eget batch-ID och gör följande begäran.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett `_links` objekt. I objektet finns ett `_links` objekt `href` med ett nytt API-anrop som värde. Kopiera det här värdet för att fortsätta till nästa steg.

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

Använd det `href` värde du fick i föregående steg som ett API-anrop för att göra en ny GET-förfrågan om att hämta din filkatalog.

**API-format**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href` värdet från [föregående steg](#retrieve-the-next-api-call-with-your-batch-id). Den är också tillgänglig i `data` arrayen under objekttypen `dataSetFileId`. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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


Kopiera `href` värdet för alla filobjekt i `data` arrayen och fortsätt till nästa steg.

## Hämta fildata

Om du vill hämta fildata skickar du en GET till det `"href"` värde du kopierade i föregående steg när du [hämtade filerna](#retrieving-your-files).

>[!NOTE]
>
>Om du gör den här begäran direkt i kommandoraden kanske du uppmanas att lägga till en utdatafil efter rubrikerna i din begäran. Följande exempel på begäran använder `--output {FILENAME.FILETYPE}`.

**API-format**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href` värdet från ett [tidigare steg](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Filens namn. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Ett annat sätt att ladda ned poängdata är att exportera målgruppen till en datauppsättning. När ett segmenteringsjobb har slutförts (värdet för `status` attributet är &quot;SUCCEEDED&quot;) kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras. Mer information om segmentering finns i [segmenteringsöversikten](../../../segmentation/home.md).

>[!IMPORTANT]
>
>För att den här exportmetoden ska kunna användas måste kundprofilen i realtid aktiveras för datauppsättningen.

Avsnittet [Exportera ett segment](../../../segmentation/tutorials/evaluate-a-segment.md) i segmentutvärderingsguiden innehåller de steg som krävs för att exportera en målgruppsdatauppsättning. Stödlinjen innehåller konturer och exempel på följande:

- **Skapa en måldatauppsättning:** Skapa datauppsättningen för målgruppsmedlemmar.
- **Generera målgruppsprofiler i datauppsättningen:** Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- **Övervaka exportförlopp:** Kontrollera exportförloppet.
- **Läs målgruppsdata:** Hämta de resulterande enskilda XDM-profilerna som representerar medlemmarna i din publik.

## Nästa steg

I det här dokumentet beskrivs stegen som krävs för att hämta AI-poäng för kunder. Nu kan du fortsätta att söka bland de andra [intelligenta tjänsterna](../../home.md) och guiderna som erbjuds.
