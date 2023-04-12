---
keywords: Experience Platform;hem;populära ämnen;filter;filter;filterdata;Filterdata;datumintervall
solution: Experience Platform
title: Filtrera katalogdata med hjälp av frågeparametrar
description: Med Catalog Service API kan svarsdata filtreras med hjälp av frågeparametrar. En del av de bästa sätten för Catalog är att använda filter i alla API-anrop, eftersom de minskar belastningen på API:t och bidrar till att förbättra prestanda generellt.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 0%

---

# Filter [!DNL Catalog] data med frågeparametrar

The [!DNL Catalog Service] API tillåter att svarsdata filtreras med hjälp av frågeparametrar. En del av bästa praxis för [!DNL Catalog] är att använda filter i alla API-anrop, eftersom de minskar belastningen på API:t och bidrar till att förbättra den övergripande prestandan.

Det här dokumentet innehåller de vanligaste filtreringsmetoderna [!DNL Catalog] -objekt i API:t. Vi rekommenderar att du refererar till det här dokumentet när du läser [Utvecklarhandbok för kataloger](getting-started.md) om du vill veta mer om hur du interagerar med [!DNL Catalog] API. Mer allmän information om [!DNL Catalog Service], se [[!DNL Catalog] översikt](../home.md).

## Begränsa returnerade objekt

The `limit` frågeparametern begränsar antalet objekt som returneras i ett svar. [!DNL Catalog] svaren mäts automatiskt i enlighet med de konfigurerade gränserna:

* Om en `limit` ingen parameter har angetts, det maximala antalet objekt per svarsnyttolast är 20.
* För datauppsättningsfrågor, om `observableSchema` begärs med `properties` frågeparameter, det maximala antalet returnerade datauppsättningar är 20.
* Den globala gränsen för alla andra katalogfrågor är 100 objekt.
* Ogiltig `limit` parametrar (inklusive `limit=0`) resulterar i 400-nivåfel som anger rätt intervall.
* Gränser eller förskjutningar som skickas som frågeparametrar har företräde framför de som skickas som rubriker.

**API-format**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Ett heltal som anger antalet objekt som ska returneras, från 1 till 100. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar samtidigt som svaret begränsas till tre objekt.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med datauppsättningar, begränsad till det antal som anges av `limit` frågeparameter.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Begränsa visade egenskaper

Även vid filtrering av antalet objekt som returneras med `limit` -parametern kan de returnerade objekten i sig ofta innehålla mer information än du behöver. För att ytterligare minska belastningen på systemet är det bäst att filtrera svaren så att de bara innehåller de egenskaper som du behöver.

The `properties` parameterfiltrerar svarsobjekt så att bara en uppsättning angivna egenskaper returneras. Parametern kan ställas in så att den returnerar en eller flera egenskaper.

The `properties` parametern accepterar bara objektegenskaper på den översta nivån, vilket innebär att du kan använda filter för följande exempelobjekt `name`, `description`och `subItem`, men INTE för `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-format**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Namnet på ett attribut som ska inkluderas i svarstexten. |
| `{OBJECT_ID}` | Unik identifierare för en specifik [!DNL Catalog] objekt som hämtas. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar. Den kommaavgränsade listan med egenskapsnamn som anges under `properties` parameter anger de egenskaper som ska returneras i svaret. A `limit` parametern ingår också, vilket begränsar antalet returnerade datauppsättningar. Om begäran inte innehöll en `limit` -parametern innehåller svaret högst 20 objekt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med [!DNL Catalog] objekt där endast de begärda egenskaperna visas.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

Baserat på ovanstående svar kan man dra slutsatsen följande:

* Om ett objekt saknar begärda egenskaper visas endast de begärda egenskaper som det innehåller. (`Dataset1`)
* Om ett objekt inte innehåller någon av de begärda egenskaperna visas det som ett tomt objekt. (`Dataset2`)
* En datauppsättning kan returnera en begärd egenskap som ett tomt objekt om den innehåller egenskapen men det inte finns något värde. (`Dataset3`)
* Annars visar datauppsättningen det fullständiga värdet för alla begärda egenskaper. (`Dataset4`)

>[!NOTE]
>
>I `schemaRef` för varje datauppsättning, versionsnumret anger den senaste delversionen av schemat. Se avsnittet om [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden för mer information.

## Startindex för förskjutning av svarslista

The `start` frågeparametern förskjuter svarslistan framåt med ett angivet nummer, med hjälp av nollbaserad numrering. Till exempel: `start=2` skulle förskjuta svaret så att det startar på det tredje listade objektet.

Om `start` parametern är inte kopplad till en `limit` -parametern är det maximala antalet returnerade objekt 20.

**API-format**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av katalogobjekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Ett heltal som anger antalet objekt som svaret ska förskjutas med. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar, som förskjuter det femte objektet (`start=4`) och begränsa svaret till två returnerade datauppsättningar (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller ett JSON-objekt som innehåller två objekt på den översta nivån (`limit=2`), en för varje datauppsättning och deras detaljer (detaljerna har komprimerats i exemplet). Svaret ändras med fyra (`start=4`), vilket innebär att de data som visas är nummer fem och sex kronologiskt.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrera efter tagg

Vissa katalogobjekt stöder användning av en `tags` -attribut. Taggar kan bifoga information till ett objekt och sedan användas för att hämta objektet. Vilka taggar som ska användas och hur de ska användas beror på organisationens processer.

Det finns några begränsningar att tänka på när du använder taggar:

* De enda katalogobjekt som för närvarande stöder taggar är datamängder, grupper och anslutningar.
* Taggnamnen är unika för din organisation.
* Adobe kan använda taggar för vissa beteenden. Namnen på dessa taggar har prefixet&quot;adobe&quot; som standard. Därför bör du undvika den här regeln när du deklarerar taggnamn.
* Följande taggnamn är reserverade för användning i [!DNL Experience Platform]och kan därför inte deklareras som ett taggnamn för din organisation:
   * `unifiedProfile`: Det här taggnamnet är reserverat för datauppsättningar som ska importeras av [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Det här taggnamnet är reserverat för datauppsättningar som ska importeras av [[!DNL Identity Service]](../../identity-service/home.md).

Nedan visas ett exempel på en datauppsättning som innehåller en `tags` -egenskap. Taggarna i den egenskapen har formen av nyckelvärdepar, där varje taggvärde visas som en array som innehåller en enda sträng:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API-format**

Värden för `tags` parametern har formen av nyckelvärdepar, med formatet `{TAG_NAME}:{TAG_VALUE}`. Flera nyckelvärdepar kan anges i form av en kommaavgränsad lista. När flera taggar anges antas en AND-relation.

Parametern stöder jokertecken (`*`) för taggvärden. En söksträng med `test*` returnerar alla objekt där taggvärdet börjar med &quot;test&quot;. En söksträng som endast består av ett jokertecken kan användas för att filtrera objekt baserat på om de innehåller en viss tagg eller inte, oavsett dess värde.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Namnet på taggen som ska filtreras efter. |
| `{TAG_VALUE}` | Värdet på taggen som ska filtreras efter. Stöder jokertecken (`*`). |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar, filtrerar efter en tagg med ett specifikt värde OCH den andra taggen finns.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en lista med datauppsättningar som innehåller `sampleTag` med värdet &quot;123456&quot;, AND `secondTag` med vilket värde som helst. Om inte en gräns också anges innehåller svaret högst 20 objekt.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrera efter datumintervall

Vissa slutpunkter i [!DNL Catalog] API har frågeparametrar som tillåter intervallfrågor, oftast för datum.

**API-format**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{TIMESTAMP }` | Ett datetime-heltal i Unix Epoch-tid. |

**Begäran**

Följande begäran hämtar en lista över batchar som skapats under april 2019.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar innehåller en lista med [!DNL Catalog] objekt som ligger inom det angivna datumintervallet. Om inte en gräns också anges innehåller svaret högst 20 objekt.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Sortera efter egenskap

The `orderBy` Med frågeparametern kan du sortera (ordna) svarsdata baserat på ett angivet egenskapsvärde. Den här parametern kräver en &quot;direction&quot; (`asc` för stigande eller `desc` för fallande), följt av ett kolon (`:`) och sedan en egenskap som du vill sortera resultaten efter. Om ingen riktning anges kommer standardriktningen att bli stigande.

Flera sorteringsegenskaper kan anges i en kommaseparerad lista. Om den första sorteringsegenskapen skapar flera objekt som innehåller samma värde för den egenskapen, används den andra sorteringsegenskapen för att ytterligare sortera de matchande objekten.

Ta till exempel följande fråga: `orderBy=name,desc:created`. Resultaten sorteras i stigande ordning baserat på den första sorteringsegenskapen. `name`. I fall där flera poster delar samma `name` -egenskapen sorteras de matchande posterna sedan efter den andra sorteringsegenskapen, `created`. Om inga returnerade poster delar samma `name`, `created` egenskapen spelar ingen roll i sorteringen.


**API-format**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av katalogobjekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Namnet på en egenskap som resultaten ska sorteras efter. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar sorterade efter deras `name` -egenskap. Om någon datauppsättning delar samma `name`, kommer dessa datauppsättningar i sin tur att beställas av deras `updated` i fallande ordning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar innehåller en lista med [!DNL Catalog] objekt som är sorterade enligt `orderBy` parameter. Om inte en gräns också anges innehåller svaret högst 20 objekt.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filtrera efter egenskap

[!DNL Catalog] innehåller två metoder för att filtrera efter egenskap, som beskrivs ytterligare i följande avsnitt:

* [Använda enkla filter](#using-simple-filters): Filtrera efter om en viss egenskap matchar ett visst värde.
* [Använda egenskapsparametern](#using-the-property-parameter): Använd villkorsuttryck för att filtrera baserat på om det finns en egenskap eller om en egenskaps värde matchar, approximerar eller jämför med ett annat angivet värde eller reguljärt uttryck.

### Använda enkla filter {#using-simple-filters}

Med enkla filter kan du filtrera svar baserat på specifika egenskapsvärden. Ett enkelt filter har formen av `{PROPERTY_NAME}={VALUE}`.

Frågan `name=exampleName` returnerar endast objekt vars `name` egenskapen innehåller värdet &quot;exampleName&quot;. Däremot är frågan `name=!exampleName` returnerar endast objekt vars `name` egenskapen är **not** &quot;exampleName&quot;.

Dessutom har enkla filter stöd för att fråga efter flera värden för en enda egenskap. När flera värden anges returnerar svaret objekt vars egenskap matchar **alla** av värdena i den angivna listan. Du kan invertera en fråga med flera värden genom att använda ett prefix `!` tecken till listan, endast objekt vars egenskapsvärde är **not** i den angivna listan (t.ex. `name=!exampleName,anotherName`).

**API-format**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Namnet på den egenskap vars värde du vill filtrera efter. |
| `{VALUE}` | Ett egenskapsvärde som avgör vilka resultat som ska inkluderas (eller exkluderas, beroende på frågan). |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar, filtrerad så att den endast innehåller datauppsättningar vars `name` -egenskapen har värdet &quot;exampleName&quot; eller &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar innehåller en lista med datauppsättningar, exklusive datauppsättningar vars `name` är &quot;exampleName&quot; eller &quot;anotherName&quot;. Om inte en gräns också anges innehåller svaret högst 20 objekt.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Använda `property` parameter {#using-the-property-parameter}

The `property` frågeparametern ger större flexibilitet för egenskapsbaserad filtrering än enkla filter. Förutom att filtrera baserat på om en egenskap har ett visst värde, kan `property` parametern kan använda andra jämförelseoperatorer (till exempel&quot;mer än&quot;)`>`) och &quot;mindre än&quot; (`<`)) samt reguljära uttryck för att filtrera efter egenskapsvärden. Det kan också filtrera efter om en egenskap finns eller inte, oavsett dess värde.

The `property` parametern accepterar bara objektegenskaper på den översta nivån, vilket innebär att du för följande exempelobjekt kan filtrera efter egenskap för `name`, `description`och `subItem`, men INTE för `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-format**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Typ av [!DNL Catalog] objekt som ska hämtas. Giltiga objekt är: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Ett villkorsuttryck som anger vilken egenskap som ska efterfrågas och hur dess värde ska utvärderas. Nedan finns exempel. |

Värdet för `property` -parametern stöder flera olika typer av villkorsuttryck. I följande tabell visas den grundläggande syntaxen för uttryck som stöds:

| Symbol(er) | Beskrivning | Exempel |
| --- | --- | --- |
| (Ingen) | Om du anger egenskapsnamnet utan operator returneras bara objekt där egenskapen finns, oavsett dess värde. | `property=name` |
| ! | Prefixera ett`!`&quot; till värdet av `property` parametern returnerar bara objekt där egenskapen gör det **not** finns. | `property=!name` |
| ~ | Returnerar endast objekt vars egenskapsvärden (sträng) matchar ett reguljärt uttryck som anges efter tilde (`~`). | `property=name~^example` |
| == | Returnerar endast objekt vars egenskapsvärden exakt matchar strängen som anges efter double-equals-symbolen (`==`). | `property=name==exampleName` |
| != | Returnerar endast objekt vars egenskapsvärden gör det **not** matchningssträng som anges efter symbolen not-equals (`!=`). | `property=name!=exampleName` |
| &lt; | Returnerar endast objekt vars egenskapsvärden är mindre än (men inte lika med) ett angivet värde. | `property=version<1.0.0` |
| &lt;= | Returnerar endast objekt vars egenskapsvärden är mindre än (eller lika med) ett angivet värde. | `property=version<=1.0.0` |
| > | Returnerar endast objekt vars egenskapsvärden är större än (men inte lika med) ett angivet värde. | `property=version>1.0.0` |
| >= | Returnerar endast objekt vars egenskapsvärden är större än (eller lika med) ett angivet värde. | `property=version>=1.0.0` |

>[!NOTE]
>
>The `name` egenskapen har stöd för användning av jokertecken `*`, antingen som hela söksträngen eller som en del av den. Jokertecken matchar tomma tecken, så att söksträngen `te*st` matchar värdet &quot;test&quot;. Asterisker kan undvikas genom att fördubbla dem (`**`). En dubbel asterisk i en söksträng representerar en enkel asterisk som en litteral sträng.

**Begäran**

Följande begäran returnerar alla datauppsättningar med ett versionsnummer som är större än 1.0.3.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar innehåller en lista med datauppsättningar vars versionsnummer är större än 1.0.3. Om inte en gräns också anges innehåller svaret högst 20 objekt.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Kombinera flera filter

Använda ett et-tecken (`&`) kan du kombinera flera filter i en enda begäran. När ytterligare villkor läggs till i en begäran antas en AND-relation.

**API-format**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
