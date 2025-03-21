---
keywords: Experience Platform;hem;populära ämnen;filter;filter;filterdata;Filterdata;datumintervall
solution: Experience Platform
title: Filtrera katalogdata med hjälp av frågeparametrar
description: Använd frågeparametrar för att filtrera svarsdata i katalogtjänstens API och hämta endast den information du behöver. Använd filter på API-anrop för att minska inläsningen och förbättra prestandan, vilket ger snabbare och effektivare datahämtning.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 0%

---

# Filtrera [!DNL Catalog]-data med frågeparametrar

Om du vill förbättra prestanda och hämta relevanta resultat använder du frågeparametrar för att filtrera [!DNL Catalog Service] API-svarsdata.

Lär dig mer om vanliga filtreringsmetoder för [!DNL Catalog]-objekt i API:t. Använd det här dokumentet tillsammans med [Utvecklarhandbok för katalog](getting-started.md) om du vill ha mer information om API-interaktioner. Allmän information om [!DNL Catalog Service] finns i [[!DNL Catalog] översikten](../home.md).

## Begränsa returnerade objekt {#limit-returned-objects}

Frågeparametern `limit` begränsar antalet objekt som returneras i ett svar. [!DNL Catalog] svar följer fördefinierade gränser:

* Om parametern `limit` inte anges är det maximala antalet objekt per svar 20.
* Om `observableSchema` begärs med frågeparametern `properties` för datauppsättningsfrågor är det maximala antalet returnerade datauppsättningar 20.
* För användartoken är maxgränsen 1.
* För tjänsttoken är maxgränsen 20.
* Den globala gränsen för andra katalogfrågor är 100 objekt.
* Ogiltiga `limit`-värden (inklusive `limit=0`) resulterar i felsvar på 400-nivå som anger korrekta intervall.
* Gränser eller förskjutningar som skickas som frågeparametrar har företräde framför dem i rubriker.

**API-format**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Ett heltal som anger antalet objekt som ska returneras (intervall: 1-100). |

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

Ett lyckat svar returnerar en lista med datauppsättningar, begränsad till det antal som anges av frågeparametern `limit`.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Begränsa visade egenskaper {#limit-displayed-properties}

Även om du filtrerar antalet objekt som returneras med parametern `limit` kan de returnerade objekten ofta innehålla mer information än du faktiskt behöver. För att ytterligare minska belastningen på systemet är det bäst att filtrera svaren så att de bara innehåller de egenskaper som du behöver.

Parametern `properties` filtrerar svarsobjekt så att bara en uppsättning angivna egenskaper returneras. Parametern kan ställas in så att den returnerar en eller flera egenskaper.

Parametern `properties` kan acceptera alla nivåobjektsegenskaper. `sampleKey` kan extraheras med `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | Namnet på ett attribut som ska inkluderas i svarstexten. |
| `{OBJECT_ID}` | Den unika identifieraren för ett specifikt [!DNL Catalog]-objekt som hämtas. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar. Den kommaavgränsade listan med egenskapsnamn som anges med parametern `properties` anger vilka egenskaper som ska returneras i svaret. En `limit`-parameter ingår också, vilket begränsar antalet returnerade datauppsättningar. Om begäran inte innehöll någon `limit`-parameter skulle svaret innehålla maximalt 20 objekt.

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
>I egenskapen `schemaRef` för varje datauppsättning anger versionsnumret den senaste delversionen av schemat. Mer information finns i avsnittet [schemaversion](../../xdm/api/getting-started.md#versioning) i XDM API-guiden.

## Startindex för förskjutning av svarslista {#offset-starting-index}

Frågeparametern `start` förskjuter svarslistan framåt med ett angivet nummer, med nollbaserad numrering. `start=2` skulle till exempel förskjuta svaret så att det startar på det tredje listade objektet.

Om parametern `start` inte har parats med en `limit`-parameter är det maximala antalet returnerade objekt 20.

**API-format**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av katalogobjekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Ett heltal som anger antalet objekt som svaret ska förskjutas med. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar, som förskjuts till det femte objektet (`start=4`) och begränsar svaret till två returnerade datauppsättningar (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Svaret innehåller ett JSON-objekt som innehåller två objekt på den översta nivån (`limit=2`), ett för varje datauppsättning och deras information (detaljerna har konverterats i exemplet). Svaret ändras med fyra (`start=4`), vilket innebär att de datamängder som visas är nummer fem och sex kronologiskt.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filtrera efter tagg

Vissa katalogobjekt stöder användningen av ett `tags`-attribut. Taggar kan bifoga information till ett objekt och sedan användas för att hämta objektet. Vilka taggar som ska användas och hur de ska användas beror på organisationens processer.

Det finns några begränsningar att tänka på när du använder taggar:

* De enda katalogobjekt som för närvarande stöder taggar är datamängder, grupper och anslutningar.
* Taggnamnen är unika för din organisation.
* Adobe-processer kan utnyttja taggar för vissa beteenden. Namnen på dessa taggar har prefixet&quot;adobe&quot; som standard. Därför bör du undvika den här regeln när du deklarerar taggnamn.
* Följande taggnamn är reserverade för användning i [!DNL Experience Platform] och kan därför inte deklareras som ett taggnamn för din organisation:
   * `unifiedProfile`: Det här taggnamnet är reserverat för datauppsättningar som ska importeras av [[!DNL Real-Time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Det här taggnamnet är reserverat för datauppsättningar som ska importeras av [[!DNL Identity Service]](../../identity-service/home.md).

Nedan visas ett exempel på en datamängd som innehåller en `tags`-egenskap. Taggarna i den egenskapen har formen av nyckelvärdepar, där varje taggvärde visas som en array som innehåller en enda sträng:

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

Värdena för parametern `tags` har formen av nyckelvärdepar med formatet `{TAG_NAME}:{TAG_VALUE}`. Flera nyckelvärdepar kan anges i form av en kommaavgränsad lista. När flera taggar anges antas en AND-relation.

Parametern stöder jokertecken (`*`) för taggvärden. En söksträng på `test*` returnerar till exempel alla objekt där taggvärdet börjar med &quot;test&quot;. En söksträng som endast består av ett jokertecken kan användas för att filtrera objekt baserat på om de innehåller en viss tagg eller inte, oavsett dess värde.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
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

Ett lyckat svar returnerar en lista med datauppsättningar som innehåller `sampleTag` med värdet 123456, AND `secondTag` med valfritt värde. Om ingen gräns anges innehåller svaret högst 20 objekt.

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
    }
}
```

## Filtrera efter datumintervall

Vissa slutpunkter i API:t [!DNL Catalog] har frågeparametrar som tillåter intervallfrågor, oftast för datum.

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

Ett godkänt svar innehåller en lista med [!DNL Catalog] objekt som ligger inom det angivna datumintervallet. Om ingen gräns anges innehåller svaret högst 20 objekt.

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
    }
}
```

## Sortera efter egenskap

Med frågeparametern `orderBy` kan du sortera (ordna) svarsdata baserat på ett angivet egenskapsvärde. Den här parametern kräver &quot;direction&quot; (`asc` för stigande eller `desc` för fallande), följt av kolon (`:`) och sedan en egenskap för att sortera resultaten efter. Om ingen riktning anges kommer standardriktningen att bli stigande.

Flera sorteringsegenskaper kan anges i en kommaseparerad lista. Om den första sorteringsegenskapen skapar flera objekt som innehåller samma värde för den egenskapen, används den andra sorteringsegenskapen för att ytterligare sortera de matchande objekten.

Ta till exempel följande fråga: `orderBy=name,desc:created`. Resultaten sorteras i stigande ordning baserat på den första sorteringsegenskapen, `name`. Om flera poster delar samma `name`-egenskap sorteras de matchande posterna sedan efter den andra sorteringsegenskapen, `created`. Om inga returnerade poster delar samma `name` räknas inte egenskapen `created` in i sorteringen.


**API-format**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av katalogobjekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Namnet på en egenskap som resultaten ska sorteras efter. |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar sorterade efter deras `name`-egenskap. Om en datamängd delar samma `name`, kommer dessa datauppsättningar i sin tur att ordnas efter sin `updated` -egenskap i fallande ordning.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar innehåller en lista med [!DNL Catalog] objekt som är sorterade enligt parametern `orderBy`. Om ingen gräns anges innehåller svaret högst 20 objekt.

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
    }
}
```

## Filtrera efter egenskap

[!DNL Catalog] innehåller två metoder för att filtrera efter egenskap, som beskrivs ytterligare i följande avsnitt:

* [Använda enkla filter](#using-simple-filters): Filtrera efter om en viss egenskap matchar ett visst värde.
* [Använder egenskapsparametern](#using-the-property-parameter): Använd villkorsuttryck för att filtrera baserat på om det finns en egenskap eller om en egenskaps värde matchar, uppskattar eller jämför med ett annat angivet värde eller reguljärt uttryck.

>[!NOTE]
>
>Alla attribut i ett Catalog-objekt kan användas för att filtrera resultat i katalogtjänstens API.

### Använda enkla filter {#using-simple-filters}

Med enkla filter kan du filtrera svar baserat på specifika egenskapsvärden. Ett enkelt filter har formen `{PROPERTY_NAME}={VALUE}`.

Frågan `name=exampleName` returnerar till exempel bara objekt vars `name`-egenskap innehåller värdet &quot;exampleName&quot;. Däremot returnerar frågan `name=!exampleName` bara objekt vars `name`-egenskap är **inte** &quot;exampleName&quot;.

Dessutom har enkla filter stöd för att fråga efter flera värden för en enda egenskap. När flera värden anges returnerar svaret objekt vars egenskap matchar **valfri** av värdena i den angivna listan. Du kan invertera en fråga med flera värden genom att lägga till ett `!`-tecken i listan som prefix och bara returnera objekt vars egenskapsvärde är **inte** i den angivna listan (till exempel `name=!exampleName,anotherName`).

**API-format**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beskrivning |
| --- | --- |
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Namnet på den egenskap vars värde du vill filtrera efter. |
| `{VALUE}` | Ett egenskapsvärde som avgör vilka resultat som ska inkluderas (eller exkluderas, beroende på frågan). |

**Begäran**

Följande begäran hämtar en lista med datauppsättningar, filtrerad så att den bara innehåller datauppsättningar vars `name`-egenskap har värdet &quot;exampleName&quot; eller &quot;anotherName&quot;.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar innehåller en lista med datauppsättningar, exklusive datauppsättningar vars `name` är &quot;exampleName&quot; eller &quot;anotherName&quot;. Om ingen gräns anges innehåller svaret högst 20 objekt.

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
    }
}
```

### Använda parametern `property` {#using-the-property-parameter}

Frågeparametern `property` ger större flexibilitet för egenskapsbaserad filtrering än enkla filter. Förutom filtrering baserad på om en egenskap har ett visst värde kan parametern `property` använda andra jämförelseoperatorer (till exempel&quot;mer än&quot; (`>`) och&quot;mindre än&quot; (`<`)) samt reguljära uttryck för att filtrera efter egenskapsvärden. Det kan också filtrera efter om en egenskap finns eller inte, oavsett dess värde.

Använd ett et-tecken (`&`) om du vill kombinera flera filter och förfina frågan i en enda begäran. När du filtrerar efter flera fält används en `AND`-relation som standard.

>[!NOTE]
>
>Om du kombinerar flera `property`-parametrar i en enda fråga måste minst en gälla för fältet `id` eller `created`. Följande fråga returnerar objekt där `id` är `abc123` **AND** `name` inte är `test`:
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

Om du använder flera `property`-parametrar i samma fält börjar bara den senast angivna parametern gälla.

>[!IMPORTANT]
>
>Du **kan inte** använda en enda `property`-parameter för att filtrera flera fält samtidigt. Varje fält måste ha en egen `property`-parameter. Följande exempel (`property=id>abc,name==myDataset`) är **inte** tillåtet eftersom det försöker tillämpa villkor på `id` och `name` inom en **enkel `property`-parameter**.

Parametern `property` kan acceptera alla nivåobjektsegenskaper. `sampleKey` kan användas för filtrering med `?properties=subItem.sampleKey`.

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
| `{OBJECT_TYPE}` | Den typ av [!DNL Catalog]-objekt som ska hämtas. Giltiga objekt är: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Ett villkorsuttryck som anger vilken egenskap som ska efterfrågas och hur dess värde ska utvärderas. Nedan finns exempel. |

Värdet för parametern `property` stöder flera olika typer av villkorsuttryck. I följande tabell visas den grundläggande syntaxen för uttryck som stöds:

| Symbol(er) | Beskrivning | Exempel |
| --- | --- | --- |
| (Ingen) | Om du anger egenskapsnamnet utan operator returneras bara objekt där egenskapen finns, oavsett dess värde. | `property=name` |
| ! | Om du lägger till `!` till värdet för en `property`-parameter returneras bara objekt där egenskapen **inte** finns. | `property=!name` |
| ~ | Returnerar endast objekt vars egenskapsvärden (sträng) matchar ett reguljärt uttryck som anges efter tilde-symbolen (`~`). | `property=name~^example` |
| == | Returnerar endast objekt vars egenskapsvärden exakt matchar strängen som anges efter double-equals-symbolen (`==`). | `property=name==exampleName` |
| != | Returnerar endast objekt vars egenskapsvärden **inte** matchar strängen som anges efter symbolen not-equals (`!=`). | `property=name!=exampleName` |
| &lt; | Returnerar endast objekt vars egenskapsvärden är mindre än (men inte lika med) ett angivet värde. | `property=version<1.0.0` |
| &lt;= | Returnerar endast objekt vars egenskapsvärden är mindre än (eller lika med) ett angivet värde. | `property=version<=1.0.0` |
| > | Returnerar endast objekt vars egenskapsvärden är större än (men inte lika med) ett angivet värde. | `property=version>1.0.0` |
| >= | Returnerar endast objekt vars egenskapsvärden är större än (eller lika med) ett angivet värde. | `property=version>=1.0.0` |
| * | Ett jokertecken används för alla strängegenskaper och matchar alla teckensekvenser. Använd `**` för att undvika en literal asterisk. | `property=name==te*st` |
| &amp; | Kombinerar flera `property`-parametrar med en `AND`-relation mellan dem. | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>Egenskapen `name` stöder användningen av jokertecknet `*`, antingen som hela söksträngen eller som en del av den. Jokertecken matchar tomma tecken så att söksträngen `te*st` matchar värdet &quot;test&quot;. Asterisker kan fördubblas (`**`). En dubbel asterisk i en söksträng representerar en enkel asterisk som en litteral sträng.

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

Ett godkänt svar innehåller en lista med datauppsättningar vars versionsnummer är större än 1.0.3. Om ingen gräns anges innehåller svaret högst 20 objekt.

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
    }
}
```

## Filtrera arrayer med parametern property {#filter-arrays}

Använd operatorer för likhet och olikhet för att inkludera eller exkludera specifika värden när du filtrerar resultat baserat på arrayegenskaper.

### Likhetsfilter {#equality-filters}

Om du vill filtrera ett arrayfält efter flera värden använder du separata egenskapsparametrar för varje värde. Använd likhetsfilter om du bara vill returnera de poster i arraydata som matchar de angivna värdena.

>[!NOTE]
>
>Kravet på att inkludera `id` eller `created` vid filtrering av flera fält gäller **inte** vid filtrering av flera värden i ett matrisfält.

Exempelfrågan nedan returnerar bara resultat från den array som innehåller både `val1` och `val2`.

**API-format**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### Okvalitetsfilter {#inequality-filters}

Använd olikhetsoperatorer (`!=`) i ett matrisfält för att exkludera poster i data där matrisen innehåller de angivna värdena.

**API-format**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

Den här frågan returnerar dokument där arrayField inte innehåller `val1` eller `val2`.

### Begränsningar för likhet och olikhet {#equality-inequality-limitations}

Du kan inte använda både likhet (`=`) och olikhet (`!=`) för samma fält i en enskild fråga.
