---
keywords: Experience Platform;home;populära topics;data access;data access api;query data access
solution: Experience Platform
title: Visa datauppsättningsdata med API:t för dataåtkomst
type: Tutorial
description: Lär dig hur du hittar, får tillgång till och hämtar data som lagras i en datauppsättning med hjälp av API:t för dataåtkomst i Adobe Experience Platform. I det här dokumentet introduceras några av de unika funktionerna i API:t för dataåtkomst, som sidindelning och partiella hämtningar.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Visa datauppsättningsdata med [!DNL Data Access] API

Använd den här steg-för-steg-självstudiekursen för att lära dig hur du hittar, får åtkomst till och hämtar data som lagras i en datauppsättning med hjälp av API:t [!DNL Data Access] i Adobe Experience Platform. Det här dokumentet innehåller några av de unika funktionerna i API:t [!DNL Data Access], till exempel sidindelning och partiella hämtningar.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse för hur du skapar och fyller i en datauppsättning. Mer information finns i självstudiekursen [Skapa datauppsättning](../../catalog/datasets/create.md).

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa Experience Platform API:er.

### Läser exempel-API-anrop {#reading-sample-api-calls}

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

Om du vill anropa [!DNL Experience Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../landing/api-authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Experience Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden utförs i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Experience Platform] finns i [översiktsdokumentationen för sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare ett huvud:

- Content-Type: application/json

## Sekvensdiagram

Den här självstudien följer stegen som beskrivs i sekvensdiagrammet nedan och framhäver kärnfunktionen i API:t [!DNL Data Access].

![Ett sekvensdiagram över API-kärnfunktionen för dataåtkomst.](../images/sequence_diagram.png)

Använd API:t [!DNL Catalog] om du vill hämta information om grupper och filer. Använd API:t [!DNL Data Access] om du vill få åtkomst till och hämta dessa filer via HTTP som antingen fullständiga eller partiella hämtningar, beroende på filens storlek.

## Hitta data

Innan du kan börja använda API:t [!DNL Data Access] måste du identifiera platsen för de data som du vill komma åt. I API:t [!DNL Catalog] finns det två slutpunkter som du kan använda för att bläddra bland en organisations metadata och hämta ID:t för en grupp eller fil som du vill komma åt:

- `GET /batches`: Returnerar en lista med batchar i din organisation
- `GET /dataSetFiles`: Returnerar en lista med filer i din organisation

En omfattande lista över slutpunkter i [!DNL Catalog] API finns i [API-referensen](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Hämta en lista över batchar i din organisation

Med API:t [!DNL Catalog] kan du returnera en lista över batchar i din organisation:

**API-format**

```http
GET /batches
```

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller ett objekt som listar alla batchar som hör till organisationen, där varje toppnivåvärde representerar en batch. De enskilda batchobjekten innehåller information om den specifika gruppen. Svaret nedan har minimerats för utrymme.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtrera listan med batchar {#filter-batches-list}

Det krävs ofta filter för att hitta en viss sats för att hämta relevanta data för ett visst användningsfall. Parametrar kan läggas till i en `GET /batches`-begäran för att filtrera det returnerade svaret. Begäran nedan returnerar alla batchar som skapats efter en viss tid, inom en viss datauppsättning, sorterade efter när de skapades.

**API-format**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Starttidsstämpeln i millisekunder (till exempel 1514836799000). |
| `{DATASET_ID}` | Identifieraren för datauppsättningen. |
| `{SORT_BY}` | Sorterar svaret efter angivet värde. `desc:created` sorterar till exempel objekten efter skapandedatum i fallande ordning. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

En fullständig lista över parametrar och filter finns i [Catalog API-referensen](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Hämta en lista med alla filer som tillhör en viss grupp

Nu när du har ID:t för gruppen som du vill komma åt kan du använda API:t [!DNL Data Access] för att få en lista över filer som hör till gruppen.

**API-format**

```http
GET /batches/{BATCH_ID}/files
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchidentifierare för den batch som du försöker få åtkomst till. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `data._links.self.href` | Den URL som ska användas för att komma åt filen. |

Svaret innehåller en datamatris som visar alla filer i den angivna gruppen. Filerna refereras till av deras fil-ID, som finns under fältet `dataSetFileId`.

## Åtkomst till en fil med ett fil-ID {#access-file-with-file-id}

När du har ett unikt fil-ID kan du använda API:t [!DNL Data Access] för att få tillgång till specifik information om filen, inklusive filens namn, storlek i byte och en länk för att hämta den.

**API-format**

```http
GET /files/{FILE_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | Identifieraren för filen som du vill komma åt. |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Beroende på om fil-ID:t pekar på en enskild fil eller en katalog kan den returnerade datarrayen innehålla en enda post eller en lista med filer som tillhör den katalogen. Varje filelement innehåller information om filens namn, storlek i byte och en länk för att hämta filen.

**Fall 1: Fil-ID pekar på en enda fil**

**Svar**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
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

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | Filens namn. |
| `_links.self.href` | Den URL som filen ska hämtas från. |

**Fall 2: Fil-ID pekar på en katalog**

**Svar**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `data._links.self.href` | URL:en som den associerade filen ska hämtas från. |

Det här svaret returnerar en katalog som innehåller två separata filer, med ID:n `{FILE_ID_2}` och `{FILE_ID_3}`. I det här fallet måste du följa URL:en för varje fil för att komma åt filen.

## Hämta metadata för en fil

Du kan hämta metadata för en fil genom att göra en HEAD-begäran. Detta returnerar filens metadatahuvuden, inklusive dess storlek i byte och filformat.

**API-format**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | Filens identifierare. |
| `{FILE_NAME}` | Filnamnet (till exempel profiles.parquet) |

**Begäran**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svarshuvuden innehåller metadata för den efterfrågade filen, inklusive:

- `Content-Length`: Anger nyttolastens storlek i byte
- `Content-Type`: Anger filtypen.

## Åtkomst till innehållet i en fil

Du kan även komma åt innehållet i en fil med API:t [!DNL Data Access].

**API-format**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID}` | Filens identifierare. |
| `{FILE_NAME}` | Filnamnet (till exempel profiles.parquet). |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar filens innehåll.

## Hämta delar av innehållet i en fil {#download-partial-file-contents}

Om du vill hämta ett specifikt intervall med byte från en fil anger du ett intervallhuvud under en `GET /files/{FILE_ID}`-begäran till [!DNL Data Access] API. Om intervallet inte anges hämtas hela filen som standard av API:t.

HEAD-exemplet i det [föregående avsnittet](#retrieve-the-metadata-of-a-file) visar storleken på en viss fil i byte.

**API-format**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{FILE_ID} ` | Filens identifierare. |
| `{FILE_NAME}` | Filnamnet (till exempel profiles.parquet) |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Egenskap | Beskrivning |
| -------- | ----------- | 
| `Range: bytes=0-99` | Anger intervallet med byte som ska hämtas. Om detta inte anges hämtas hela filen av API:t. I det här exemplet hämtas de första 100 byten. |

**Svar**

Svarstexten innehåller de första 100 byten i filen (enligt vad som anges i sidhuvudet Intervall i begäran) tillsammans med HTTP-status 206 (Del av innehåll). Svaret innehåller även följande rubriker:

- Content-Length: 100 (antalet byte som returneras)
- Innehållstyp: application/parquet (en Parquet-fil begärdes, därför är svarets innehållstyp `parquet`)
- Content-Range: bytes 0-99/249058 (begärt intervall (0-99) av totalt antal byte (249058))

## Konfigurera API-svarssidnumrering {#configure-response-pagination}

Svaren i [!DNL Data Access]-API:t är sidnumrerade. Som standard är det maximala antalet poster per sida 100. Du kan ändra standardbeteendet med sidindelningsparametrar.

- `limit`: Du kan ange antalet poster per sida enligt dina krav med parametern &quot;limit&quot;.
- `start`: Förskjutningen kan anges med frågeparametern &quot;start&quot;.
- `&`: Du kan använda ett et-tecken för att kombinera flera parametrar i ett enda anrop.

**API-format**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{BATCH_ID}` | Batchidentifierare för den batch som du försöker få åtkomst till. |
| `{OFFSET}` | Angivet index för att starta resultatarrayen (till exempel start=0) |
| `{LIMIT}` | Styr hur många resultat som returneras i resultatarrayen (till exempel limit=1) |

**Begäran**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**:

Svaret innehåller en `"data"`-matris med ett enda element, enligt parametern `limit=1` för begäran. Det här elementet är ett objekt som innehåller information om den första tillgängliga filen, enligt parametern `start=0` i begäran (kom ihåg att det första elementet är &quot;0&quot; vid nollbaserad numrering).

Värdet `_links.next.href` innehåller länken till nästa sida med svar, där du kan se att parametern `start` har utvecklats till `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
