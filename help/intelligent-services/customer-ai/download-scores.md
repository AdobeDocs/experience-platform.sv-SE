---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Ladda ned bakgrundsmusik i kundens AI
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Ladda ned bakgrundsmusik i kundens AI

Det här dokumentet är en guide för nedladdning av poäng för kundens AI.

## Komma igång

Med Customer AI kan du hämta poäng i parquet-filformat. Den här självstudien kräver att du har läst och slutfört nedladdningen av AI-poängen för kunder i guiden [Komma igång](./getting-started.md) .

För att få tillgång till poäng för kunds-AI måste du dessutom ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till användarhandboken för [AI](./user-guide.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

För närvarande finns det två sätt att hämta kundens AI-poäng:

1. Om du vill hämta poängen på individuell nivå och/eller inte har kundprofilen i realtid aktiverad börjar du med att [hitta ditt datauppsättnings-ID](#dataset-id).
2. Om du har en profil aktiverad och vill hämta segment som du har konfigurerat med hjälp av kundens AI, navigerar du till [hämtningen av ett segment som har konfigurerats med kundens AI](#segment).

## Hitta ditt datauppsättnings-ID {#dataset-id}

Klicka på listrutan *Fler åtgärder* i den övre högra navigeringsfältet och välj sedan **Åtkomstpoäng** i tjänstinstansen för att få information om kundens AI-insikter.

![fler åtgärder](./images/insights/more-actions.png)

En ny dialogruta visas med en länk till dokumentationen för nedladdning av bakgrundsmusik och datauppsättnings-ID:t för den aktuella instansen. Kopiera datauppsättnings-ID:t till Urklipp och fortsätt till nästa steg.

![Datauppsättnings-ID](./images/download-scores/access-scores.png)

## Hämta ditt batch-ID

Om du använder ditt datauppsättnings-ID från föregående steg måste du ringa ett anrop till katalog-API:t för att hämta ett batch-ID. Ytterligare frågeparametrar används för detta API-anrop för att returnera en enda batch i stället för en lista med batchar som tillhör din organisation. Mer information om vilka typer av frågeparametrar som finns tillgängliga finns i guiden om [filtrering av katalogdata med hjälp av frågeparametrar](../../catalog/api/filter-data.md).

**API-format**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | Det datauppsättnings-ID som är tillgängligt i dialogrutan Åtkomstpoäng. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en nyttolast som innehåller ett ID-objekt för musikbatch. I det här exemplet är objektet `5e602f67c2f39715a87f46b1`.

Inom poängets batch-ID-objekt finns en `relatedObjects` array. Arrayen innehåller två objekt. Det första objektet har `type` värdet &quot;batch&quot; och innehåller även ett ID. I exempelsvaret nedan är batch-ID `035e2520-5e69-11ea-b624-51evfeba55d1`. Kopiera ditt batch-ID till nästa API-anrop.

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## Hämta nästa API-anrop med ditt batch-ID

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

## Hämta dina filer

Använd det `href` värde du fick i föregående steg som ett API-anrop för att skapa en ny GET-begäran för att hämta din filkatalog.

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
| `_links.self.href` | URL:en för GET-begäran som används för att hämta en fil i din katalog. |


Kopiera `href` värdet för alla filobjekt i `data` arrayen och fortsätt till nästa steg.

## Hämta fildata

Om du vill hämta fildata gör du en GET-begäran till det `"href"` värde du kopierade i föregående steg när du [hämtade dina filer](#retrieving-your-files).

>[!NOTE] Om du gör den här begäran direkt i kommandoraden kanske du uppmanas att lägga till en utdatafil efter rubrikerna i din begäran. Följande exempel på begäran använder `--output {FILENAME.FILETYPE}`.

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

>[!TIP] Kontrollera att du är i rätt katalog eller mapp som du vill att filen ska sparas i innan du gör GET-begäran.

**Svar**

Svaret hämtar filen som du begärde i din aktuella katalog. I det här exemplet är filnamnet&quot;filename.parquet&quot;.

![Terminal](./images/download-scores/response.png)

## Hämta ett segment som konfigurerats med kundens AI {#segment}

Ett annat sätt att ladda ned poängdata är att exportera målgruppen till en datauppsättning. När ett segmenteringsjobb har slutförts (värdet för `status` attributet är &quot;SUCCEEDED&quot;) kan du exportera målgruppen till en datauppsättning där den kan nås och hanteras. Mer information om segmentering finns i [segmenteringsöversikten](../../segmentation/home.md).

>[!IMPORTANT] För att den här exportmetoden ska kunna användas måste kundprofilen i realtid aktiveras för datauppsättningen.

Avsnittet [Exportera ett segment](../../segmentation/tutorials/evaluate-a-segment.md) i segmentutvärderingsguiden innehåller de steg som krävs för att exportera en målgruppsdatauppsättning. Stödlinjen innehåller konturer och exempel på följande:

- **Skapa en måldatauppsättning:** Skapa datauppsättningen för målgruppsmedlemmar.
- **Generera målgruppsprofiler i datauppsättningen:** Fyll i datauppsättningen med enskilda XDM-profiler baserat på resultatet av ett segmentjobb.
- **Övervaka exportförlopp:** Kontrollera exportförloppet.
- **Läs målgruppsdata:** Hämta de resulterande enskilda XDM-profilerna som representerar medlemmarna i din publik.

## Nästa steg

I det här dokumentet beskrivs stegen som krävs för att hämta AI-poäng för kunder. Nu kan du fortsätta att söka bland de andra [intelligenta tjänsterna](../home.md) och guiderna som erbjuds.
