---
keywords: Experience Platform;attribuering ai;åtkomstpoäng;populära ämnen;nedladdningspoäng;attribueringspoäng;export;Exportera
feature: Attribution AI
title: Hämta bakgrundsmusik i Attribution AI
topic-legacy: Downloading scores
description: Det här dokumentet är en guide för nedladdning av bakgrundsmusik för Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Hämta bakgrundsmusik i Attribution AI

Det här dokumentet är en guide för nedladdning av bakgrundsmusik för Attribution AI.

## Komma igång

Med Attribution AI kan du hämta bakgrundsmusik i filformatet Parquet. Den här självstudien kräver att du har läst och slutfört nedladdningen av bakgrundsmusik i guiden [komma igång](./getting-started.md).

För att få åtkomst till bakgrundsmusik för Attribution AI måste du dessutom ha en tjänstinstans med statusen lyckad körning tillgänglig. Om du vill skapa en ny tjänstinstans går du till [användarhandboken för Attribution AI](./user-guide.md). Om du nyligen har skapat en tjänstinstans och den fortfarande håller på att träna och betygsätta, kan du vänta i 24 timmar tills den är klar.

## Hitta ditt datauppsättnings-ID {#dataset-id}

Klicka på listrutan *Fler åtgärder* i den övre högra navigeringen och välj sedan **[!UICONTROL Access scores]** i tjänstinstansen för att få information om Attribution AI.

![fler åtgärder](./images/download-scores/more-actions.png)

En ny dialogruta visas med en länk till dokumentationen för nedladdning av bakgrundsmusik och datauppsättnings-ID:t för den aktuella instansen. Kopiera datauppsättnings-ID:t till Urklipp och fortsätt till nästa steg.

![Datauppsättnings-ID](../customer-ai/images/download-scores/access-scores.png)

## Hämta ditt batch-ID {#retrieve-your-batch-id}

Om du använder ditt datauppsättnings-ID från föregående steg måste du ringa ett anrop till katalog-API:t för att hämta ett batch-ID. Ytterligare frågeparametrar används för detta API-anrop för att returnera den senaste lyckade gruppen i stället för en lista med batchar som tillhör din organisation. Om du vill returnera ytterligare batchar ökar du talet för `limit`-frågeparametern till önskad mängd som du vill returnera. Mer information om vilka typer av frågeparametrar som finns tillgängliga finns i guiden [filtrera katalogdata med hjälp av frågeparametrar](../../catalog/api/filter-data.md).

**API-format**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASET_ID}` | Det datauppsättnings-ID som är tillgängligt i dialogrutan Åtkomstpoäng. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett batch-ID-objekt. I det här exemplet är nyckelvärdet för det returnerade objektet batch-ID `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopiera ditt batch-ID till nästa API-anrop.

>[!NOTE]
>
> Objektet `tags` har formaterats om för läsbarhet i följande svar.

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
                "id": "5e8f81cf7a4ecb28a8d85b22"
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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en nyttolast som innehåller ett `_links`-objekt. I `_links`-objektet finns ett `href`-anrop med ett nytt API-anrop som värde. Kopiera det här värdet för att fortsätta till nästa steg.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
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

Använd det `href`-värde som du fick i det föregående steget som ett API-anrop för att skapa en ny GET-begäran för att hämta din filkatalog.

**API-format**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href`-värdet från [föregående steg](#retrieve-the-next-api-call-with-your-batch-id). Den är också tillgänglig i `data`-arrayen under objekttypen `dataSetFileId`. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
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

| Parameter | Beskrivning |
| --------- | ----------- |
| `_links.self.href` | Den URL för GET-begäran som används för att hämta en fil i din katalog. |


Kopiera `href`-värdet för valfritt filobjekt i `data`-arrayen och fortsätt sedan till nästa steg.

## Hämta fildata

Om du vill hämta fildata skickar du en GET till `"href"`-värdet som du kopierade i föregående steg [när du hämtade dina filer](#retrieving-your-files).

>[!NOTE]
>
>Om du gör den här begäran direkt i kommandoraden kanske du uppmanas att lägga till en utdatafil efter rubrikerna i din begäran. I följande exempel används `--output {FILENAME.FILETYPE}`.

**API-format**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{DATASETFILE_ID}` | DataSetFile-ID returneras i `href`-värdet från ett [föregående steg](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Filens namn. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Se till att du är i rätt katalog eller mapp som du vill att filen ska sparas i innan du skickar GETEN.

**Svar**

Svaret hämtar filen som du begärde i din aktuella katalog. I det här exemplet är filnamnet&quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

Poängen som hämtas kommer att vara i Parquet-format och måste ha en [!DNL Spark]-shell- eller Parquet-läsare för att visa poängen. För visning av råa poäng kan du använda [Apache Parquet-verktygen](https://parquet.apache.org/documentation/latest/). Parquet-verktygen kan analysera data med [!DNL Spark].

## Nästa steg

I det här dokumentet beskrivs stegen som krävs för att hämta bakgrundsmusik för Attribution AI. Mer information om bakgrundsmusik finns i dokumentationen för [AI-attributindata och -utdata](./input-output.md).

## Åtkomst till bakgrundsmusik med Snowflake

>[!IMPORTANT]
>
>Kontakta attributionai-support@adobe.com om du vill ha mer information om hur du får åtkomst till bakgrundsmusik med Snowflake.

Du kan komma åt aggregerade Attribution AI via Snowflake. För närvarande måste du skicka e-post till supporten för Adobe på attributionai-support@adobe.com för att kunna konfigurera och ta emot inloggningsuppgifterna till ditt läsarkonto för Snowflake.

När supporten för Adobe har bearbetat din begäran, får du en URL för läsarkontot till Snowflake och motsvarande uppgifter nedan:

- Snowflake URL
- Användarnamn
- Lösenord

>[!NOTE]
>
>Läsarkontot används för att fråga data med SQL-klienter, kalkylblad och BI-lösningar som stöder JDBC-anslutning.

När du har dina inloggningsuppgifter och URL-adresser kan du söka efter modelltabellerna, aggregerade efter kontaktpunktsdatum eller konverteringsdatum.

### Hitta ditt schema i Snowflake

Logga in på Snowflake med de angivna inloggningsuppgifterna. Klicka på fliken **Kalkylblad** i den övre vänstra huvudnavigeringen och navigera sedan till din databaskatalog i den vänstra panelen.

![Kalkylblad och navigering](./images/download-scores/edited_snowflake_1.png)

Klicka sedan på **Välj schema** i skärmens övre högra hörn. Bekräfta att du har markerat rätt databas i den port som visas. Klicka sedan på listrutan *Schema* och välj ett av scheman i listan. Du kan söka direkt från de poängtabeller som listas under det valda schemat.

![hitta ett schema](./images/download-scores/edited_snowflake_2.png)

## Ansluta PowerBI till Snowflake (valfritt)

Dina inloggningsuppgifter för Snowflake kan användas för att skapa en anslutning mellan PowerBI Desktop och Snowflake-databaser.

I rutan *Server* skriver du Snowflake-URL:en. Skriv sedan in &quot;XSMALL&quot; under *Lagerställe*. Ange sedan ditt användarnamn och lösenord.

![exempel på POWERBI](./images/download-scores/powerbi-snowflake.png)

När anslutningen har upprättats väljer du din Snowflake-databas och väljer sedan lämpligt schema. Du kan nu läsa in alla tabeller.
