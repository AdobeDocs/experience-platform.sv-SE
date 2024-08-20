---
keywords: Experience Platform;hem;populära ämnen;ETL;etl;etl integrations;ETL integrations
solution: Experience Platform
title: Utveckla ETL-integreringar för Adobe Experience Platform
description: Integreringsguiden för ETL beskriver allmänna steg för att skapa säkra anslutningar med höga prestanda för Experience Platform och inmatning av data på plattformen.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '3977'
ht-degree: 0%

---

# Utveckla ETL-integreringar för Adobe Experience Platform

Integreringsguiden för ETL innehåller allmänna steg för att skapa säkra anslutningar med höga prestanda för [!DNL Experience Platform] och för att importera data till [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Autentisering och auktorisering för Experience Platform API:er](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Den här handboken innehåller även exempel på API-anrop som ska användas när du utformar en ETL-koppling, med länkar till dokumentation som beskriver varje [!DNL Experience Platform]-tjänst och användningen av dess API, i detalj.

En exempelintegrering är tillgänglig på [!DNL GitHub] via [ETL Ecosystem Integration Reference Code ](https://github.com/adobe/acp-data-services-etl-reference) under [!DNL Apache] License Version 2.0.

## Arbetsflöde

Följande arbetsflödesdiagram ger en översikt på hög nivå över integrationen av Adobe Experience Platform-komponenter med ett ETL-program och en ETL-anslutning.

![](images/etl.png)

## Adobe Experience Platform-komponenter

Det finns flera Experience Platform-komponenter som ingår i ETL-anslutningsintegreringar. I följande lista beskrivs flera viktiga komponenter och funktioner:

- **Adobe Identity Management System (IMS)** - Tillhandahåller ramverk för autentisering till Adobe-tjänster.
- **IMS-organisation** - En företagsenhet som kan äga eller licensiera produkter och tjänster och tillåta åtkomst till medlemmarna.
- **IMS-användare** - medlemmar i en IMS-organisation. Relationen organisation till användare är många för många.
- **[!DNL Sandbox]** - En virtuell partition är en enda [!DNL Platform]-instans som hjälper dig att utveckla och utveckla program för digitala upplevelser.
- **Dataidentifiering** - Registrerar metadata för inkapslade och omformade data i [!DNL Experience Platform].
- **[!DNL Data Access]** - Ger användare ett gränssnitt för att komma åt data i [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Skickar data till [!DNL Experience Platform] med [!DNL Data Ingestion] API:er.
- **[!DNL Schema Registry]** - Definierar och lagrar schema som beskriver strukturen för data som ska användas i [!DNL Experience Platform].

## Komma igång med [!DNL Experience Platform] API:er

I följande avsnitt finns ytterligare information som du behöver känna till eller ha till hands för att kunna anropa [!DNL Experience Platform] API:er.

### Läser exempel-API-anrop

Den här guiden innehåller exempel på API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [Så här läser du exempel-API-anrop](../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för [!DNL Experience Platform].

### Samla in värden för obligatoriska rubriker

För att kunna anropa [!DNL Platform] API:er måste du först slutföra [autentiseringssjälvstudiekursen](https://www.adobe.com/go/platform-api-authentication-en). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla [!DNL Experience Platform] API-anrop, vilket visas nedan:

- Behörighet: Bärare `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alla resurser i [!DNL Experience Platform] är isolerade till specifika virtuella sandlådor. Alla begäranden till [!DNL Platform] API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i [!DNL Platform] finns i [översiktsdokumentationen för sandlådan](../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Content-Type: application/json

## Allmänt användarflöde

Till att börja med loggar en ETL-användare in i användargränssnittet för [!DNL Experience Platform] och skapar datauppsättningar för förtäring med hjälp av en standardanslutning eller en push-tjänstanslutning.

I användargränssnittet skapar användaren utdata genom att välja ett dataschema. Vilket schema som väljs beror på vilken typ av data (post- eller tidsserie) som hämtas till [!DNL Platform]. Genom att klicka på fliken Scheman i användargränssnittet kan användaren visa alla tillgängliga scheman, inklusive den beteendetyp som schemat stöder.

I ETL-verktyget kommer användaren att börja designa sina mappningstransformeringar efter att ha konfigurerat lämplig anslutning (med hjälp av sina autentiseringsuppgifter). ETL-verktyget antas redan ha [!DNL Experience Platform] anslutningar installerade (processen är inte definierad i den här integreringshandboken).

Kopplingar för ett ETL-exempelverktyg och arbetsflöde har angetts i [ETL-arbetsflödet](./workflow.md). ETL-verktygen kan ha olika format, men de flesta visar liknande funktioner.

>[!NOTE]
>
>ETL-kopplingen måste ange ett tidsstämpelfilter som markerar datumet för att importera data och förskjutning (dvs. Fönstret som data ska läsas för). ETL-verktyget bör ha stöd för att ta dessa två parametrar i det här eller ett annat relevant gränssnitt. I Adobe Experience Platform mappas de här parametrarna till antingen tillgängliga datum (om sådana finns) eller inhämtningsdatum i ett batchobjekt i datauppsättningen.

### Visa lista med datauppsättningar

Med datakällan för mappning kan en lista över alla tillgängliga datauppsättningar hämtas med [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

Du kan utfärda en enda API-begäran för att visa alla tillgängliga datauppsättningar (t.ex. `GET /dataSets`). Bästa praxis är att inkludera frågeparametrar som begränsar svarsstorleken.

Om fullständig datauppsättningsinformation begärs kan svarsnyttolasten nå över 3 GB, vilket kan försämra den totala prestandan. Om du använder frågeparametrar för att filtrera endast den information som behövs blir [!DNL Catalog] frågor därför mer effektiva.

#### Listfiltrering

När du filtrerar svar kan du använda flera filter i ett enda anrop genom att separera parametrar med ett et-tecken (`&`). Vissa frågeparametrar accepterar kommaseparerade värdelistor, t.ex. &quot;properties&quot;-filtret i exempelbegäran nedan.

[!DNL Catalog] svar mäts automatiskt enligt konfigurerade gränser, men frågeparametern &quot;limit&quot; kan användas för att anpassa begränsningarna och begränsa antalet returnerade objekt. De förkonfigurerade svarsgränserna för [!DNL Catalog] är:

- Om ingen gränsparameter anges är det maximala antalet objekt per svarsnyttolast 20.
- Den globala gränsen för alla andra [!DNL Catalog]-frågor är 100 objekt.
- Om du begär observerableSchema med frågeparametern properties för datauppsättningsfrågor är det maximala antalet returnerade datauppsättningar 20.
- Ogiltiga gränsparametrar (inklusive `limit=0`) uppfylls med ett HTTP 400-fel som anger korrekta intervall.
- Om gränser eller förskjutningar skickas som frågeparametrar har de företräde framför dem som skickas som rubriker.

Frågeparametrar beskrivs mer ingående i [Katalogtjänstöversikt](../catalog/home.md).

**API-format**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

I [Katalogtjänstöversikten](../catalog/home.md) finns detaljerade exempel på hur du anropar [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Svar**

Svaret innehåller tre (`limit=3`) datamängder som visar &quot;name&quot;, &quot;description&quot; och &quot;schemaRef&quot; enligt frågeparametern `properties`.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Visa dataschema

Egenskapen schemaRef för en datamängd innehåller en URI som refererar till det XDM-schema som datamängden baseras på. XDM-schemat (&quot;schemaRef&quot;) representerar alla möjliga fält som kan användas av datauppsättningen, inte nödvändigtvis de fält som används (se &quot;observerableSchema&quot; nedan).

XDM-schemat är det schema som du använder när du behöver visa en lista över alla tillgängliga fält som kan skrivas till användaren.

Det första värdet för schemaRef.id i det föregående svarsobjektet (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) är en URI som pekar på ett specifikt XDM-schema i [!DNL Schema Registry]. Schemat kan hämtas genom att en sökbegäran (GET) görs till API:t [!DNL Schema Registry].

>[!NOTE]
>
>Egenskapen &quot;schemaRef&quot; ersätter den nu inaktuella egenskapen &quot;schema&quot;. Om &quot;schemaRef&quot; saknas i datauppsättningen eller inte innehåller något värde, måste du kontrollera om det finns en &quot;schema&quot;-egenskap. Detta kan göras genom att ersätta &quot;schemaRef&quot; med &quot;schema&quot; i frågeparametern `properties` i det föregående anropet. Mer information om schemaegenskapen finns i avsnittet [Schemaegenskap för datauppsättning](#dataset-schema-property-deprecated---eol-2019-05-30) som följer.

**API-format**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Begäran**

Begäran använder URL-kodad `id` URI för schemat (värdet för attributet schemaRef.id) och kräver en Accept-rubrik.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Svarsformatet beror på vilken typ av Acceptera-huvud som skickas i begäran. Uppslagsbegäranden kräver också att `version` inkluderas i huvudet Godkänn. Följande tabell visar tillgängliga Accept headers för uppslag:

| Acceptera | Beskrivning |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Lista (GET) över förfrågningar, titlar, id:n och versioner |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs och allOf resolved, har titlar och beskrivningar |
| `application/vnd.adobe.xed+json; version={major version}` | Raw med $ref och allOf, har rubriker och beskrivningar |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw med $ref och allOf, inga titlar eller beskrivningar |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs och allOf resolved, inga titlar eller beskrivningar |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs och allOf resolved, descriptor included |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` och `application/vnd.adobe.xed-full+json; version={major version}` är de vanligaste Acceptera rubrikerna. `application/vnd.adobe.xed-id+json` är att föredra om du vill visa resurser i [!DNL Schema Registry], eftersom det bara returnerar &quot;title&quot;, &quot;id&quot; och &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` är att föredra när du vill visa en specifik resurs (med dess &quot;id&quot;) eftersom den returnerar alla fält (kapslade under &quot;properties&quot;) samt rubriker och beskrivningar.

**Svar**

Det returnerade JSON-schemat beskriver strukturen och fältnivåinformationen (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, etc.) av data, serialiserat som JSON. Om du använder ett annat serialiseringsformat än JSON för förtäring (till exempel Parquet eller Scala) innehåller [schematabellguiden](../xdm/tutorials/create-schema-api.md) en tabell som visar önskad JSON-typ (&quot;meta:xdmType&quot;) och dess motsvarande representation i andra format.

Tillsammans med den här tabellen innehåller utvecklarhandboken för [!DNL Schema Registry] detaljerade exempel på alla anrop som kan göras med API:t [!DNL Schema Registry].

### Datauppsättningens schemaegenskap (DEPRECATED - EOL 2019-05-30)

Datauppsättningar kan innehålla en schemaegenskap som nu är föråldrad och som tillfälligt är tillgänglig för bakåtkompatibilitet. En listbegäran (GET) som liknar den som gjordes tidigare, där &quot;schema&quot; ersattes med &quot;schemaRef&quot; i frågeparametern `properties`, kan returnera följande:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Om schemaegenskapen för en datauppsättning fylls i signalerar detta att schemat är ett inaktuellt `/xdms`-schema och, om det stöds, ska ETL-kopplingen använda värdet i schemaegenskapen med `/xdms`-slutpunkten (en inaktuell slutpunkt i [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) för att hämta det äldre schemat.

**API-format**

```http
GET /catalog/{"schema" property without the "@"}
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>En valfri frågeparameter, `expansion=xdm`, anger att API:t ska expandera och infoga alla refererade scheman. Du kanske vill göra detta när du visar en lista över alla möjliga fält för användaren.

**Svar**

Ungefär som stegen för [visning av datamängdsschema](#view-dataset-schema) innehåller svaret ett JSON-schema som beskriver strukturen och fältnivåinformationen för data, serialiserat som JSON.

>[!NOTE]
>
>När schemafältet är tomt eller helt saknas, bör kopplingen läsa fältet &quot;schemaRef&quot; och använda [API:t för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/) som i föregående steg för att [visa ett datamängdsschema](#view-dataset-schema).

### Egenskapen &quot;observerableSchema&quot;

Egenskapen &quot;observerableSchema&quot; för en datauppsättning har en JSON-struktur som matchar XDM-schemats JSON. &quot;observerableSchema&quot; innehåller fälten som fanns i de inkommande indatafilerna. När data skrivs till [!DNL Experience Platform] behöver en användare inte använda alla fält från målschemat. I stället bör de bara ange de fält som används.

Det observerbara schemat är det schema som du skulle använda om du läste data eller presenterade en lista med fält som är tillgängliga att läsa/mappa från.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Förhandsgranska data

ETL-programmet kan ge möjlighet att förhandsgranska data ([&quot;Bild 8&quot; i ETL-arbetsflödet ](./workflow.md)). API:t för dataåtkomst innehåller flera alternativ för att förhandsgranska data.

Ytterligare information, inklusive stegvisa anvisningar för att förhandsgranska data med hjälp av API:t för dataåtkomst, finns i [dataåtkomstsjälvstudiekursen](../data-access/tutorials/dataset-data.md).

### Hämta datauppsättningsinformation med frågeparametern &quot;properties&quot;

Så som visas i stegen ovan för att [visa en lista med datauppsättningar](#view-list-of-datasets) kan du begära &quot;filer&quot; med frågeparametern &quot;properties&quot;.

Mer information om hur du frågar efter datauppsättningar och tillgängliga svarsfilter finns i [Katalogtjänstöversikten](../catalog/home.md).

**API-format**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Svar**

Svaret innehåller en datauppsättning (`limit=1`) som visar egenskapen &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
  }
}
```

### Visa datauppsättningsfiler med attributet &quot;files&quot;

Du kan också använda en GET-begäran för att hämta filinformation med attributet &quot;files&quot;.

**API-format**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

Svaret inkluderar datauppsättningens fil-ID som den översta egenskapen, med filinformation som finns i datauppsättningens fil-ID-objekt.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Hämta filinformation

De datauppsättningsfil-ID som returnerades i det föregående svaret kan användas i en GET-begäran för att hämta ytterligare filinformation via API:t [!DNL Data Access].

[Dataåtkomstöversikten](../data-access/home.md) innehåller information om hur du använder API:t [!DNL Data Access].

**API-format**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Förhandsgranska fildata

Egenskapen href kan användas för att hämta förhandsgranskningsdata via [[!DNL Data Access API]](../data-access/home.md).

**API-format**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Svaret på ovanstående begäran innehåller en förhandsgranskning av filens innehåll.

Mer information om API:t [!DNL Data Access], inklusive detaljerade begäranden och svar, finns i [dataåtkomstöversikten](../data-access/home.md).

### Hämta fileDescription från datauppsättningen

Målkomponenten är utdata från omformade data och datateknikern väljer en utdatauppsättning ([&quot;Figur 12&quot; i ETL-arbetsflödet ](workflow.md)). XDM-schemat är associerat med utdatauppsättningen. De data som ska skrivas identifieras av attributet &quot;fileDescription&quot; för datauppsättningsentiteten från API:erna för dataidentifiering. Den här informationen kan hämtas med ett datauppsättnings-ID (`{DATASET_ID}`). Egenskapen fileDescription i JSON-svaret innehåller den begärda informationen.

**API-format**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `{DATASET_ID}` | Värdet `id` för datauppsättningen som du försöker komma åt. |

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Svar**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Data skrivs till [!DNL Experience Platform] med [API:t för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  Att skriva data är en asynkron process. När data skrivs till Adobe Experience Platform skapas en batch som markeras som lyckad först när alla data är skrivna.

Data i [!DNL Experience Platform] ska skrivas i form av Parquet-filer.

## Körningsfas

När körningen startar kommer kopplingen (enligt definitionen i källkomponenten) att läsa data från [!DNL Experience Platform] med hjälp av [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Omvandlingsprocessen läser data för ett visst tidsintervall. Internt kommer programmet att fråga batchar med källdataset. Vid sökning används en parametriserad (rullande för tidsseriedata eller inkrementella data) startdatum och listdatauppsättningsfiler för dessa grupper, och begäran om data för dessa datauppsättningsfiler börjar.

### Exempelomformningar

[Exempeldokumentet för ETL-omformningar](./transformations.md) innehåller ett antal exempelomformningar, inklusive identitetshantering och datatypsmappningar. Använd dessa omformningar som referens.

### Läs data från [!DNL Experience Platform]

Med [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/) kan du hämta alla batchar mellan en angiven starttid och sluttid och sortera dem i den ordning de skapades.

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Information om filtrering av grupper finns i [dataåtkomstsjälvstudiekursen](../data-access/tutorials/dataset-data.md).

### Hämta filer från en grupp

När du har ID:t för gruppen som du söker efter (`{BATCH_ID}`) är det möjligt att hämta en lista över filer som tillhör en viss grupp via [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Information om hur du gör detta finns i [[!DNL Data Access] självstudiekursen](../data-access/tutorials/dataset-data.md).

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Åtkomst till filer med fil-ID

Med hjälp av ett unikt ID för en fil (`{FILE_ID`) kan [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) användas för att komma åt den specifika informationen för filen, inklusive filens namn, storlek i byte och en länk för att hämta den.

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Svaret kan peka på en enskild fil eller en katalog. Mer information finns i [[!DNL Data Access] självstudiekursen](../data-access/tutorials/dataset-data.md).

### Åtkomst till filinnehåll

[[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) kan användas för att komma åt innehållet i en viss fil. För att hämta innehållet görs en GET-förfrågan med det värde som returnerats för `_links.self.href` vid åtkomst av en fil med fil-ID.

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Svaret på den här begäran innehåller innehållet i filen. Mer information, inklusive information om svarssidnumrering, finns i självstudiekursen [Fråga data via API för dataåtkomst](../data-access/tutorials/dataset-data.md).

### Validera poster för schemakompatibilitet

När data skrivs kan användarna välja att validera data enligt de valideringsregler som definieras i XDM-schemat. Mer information om schemavalidering finns i [ETL Ecosystem Integration Reference Code på  [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Om du använder den referensimplementering som finns på [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md) kan du aktivera schemavalidering i den här implementeringen med hjälp av systemegenskapen `-DenableSchemaValidation=true`.

Validering kan utföras för logiska XDM-typer, med attribut som `minLength` och `maxlength` för strängar, `minimum` och `maximum` för heltal, med mera. Utvecklarhandboken för [Schema Registry API](../xdm/api/getting-started.md) innehåller en tabell som visar XDM-typer och de egenskaper som kan användas för validering.

>[!NOTE]
>
>Minimi- och maximivärdena som anges för olika `integer`-typer är de MIN- och MAX-värden som typen kan hantera, men dessa värden kan begränsas ytterligare till de minimi- och maximivärden som du väljer.

### Skapa en batch

När data har bearbetats skriver ETL-verktyget tillbaka data till [!DNL Experience Platform] med [API:t för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Innan data kan läggas till i en datauppsättning måste de länkas till en batch som senare överförs till en specifik datauppsättning.

**Begäran**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Information om hur du skapar en grupp, inklusive exempelbegäranden och svar, finns i översikten [Gruppinmatning](../ingestion/batch-ingestion/overview.md).

### Skriv till datauppsättning

När en ny grupp har skapats kan filer sedan överföras till en viss datauppsättning. Flera filer kan publiceras i en grupp tills den befordras. Filer kan överföras med API:t för liten filöverföring. Om filerna är för stora och gatewaygränsen överskrids kan du använda API:t för stor filöverföring. Information om hur du använder både stor och liten filöverföring finns i [översikten över gruppinmatning](../ingestion/batch-ingestion/overview.md).

**Begäran**

Data i [!DNL Experience Platform] ska skrivas i form av Parquet-filer.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Markera batchöverföring slutförd

När alla filer har överförts till gruppen kan gruppen signaleras för slutförande. På så sätt skapas [!DNL Catalog] &quot;DataSetFile&quot;-posterna för de slutförda filerna och kopplas till genereringsgruppen. Batchen [!DNL Catalog] markeras sedan som lyckad, vilket utlöser flödesomformningar för att importera tillgängliga data.

Data kommer först att landas på mellanlagringsplatsen på Adobe Experience Platform och sedan flyttas till den slutliga platsen efter katalogisering och validering. Batchar markeras som lyckade när alla data har flyttats till en permanent plats.

**Begäran**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Om det lyckas returnerar svaret HTTP-status 200 OK och svarstexten är tom.

ETL-verktyget ser till att du noterar tidsstämpeln för källdatauppsättningar när data läses.

I nästa omformningskörning, troligtvis genom schema eller händelseanrop, börjar ETL begära data från den tidigare sparade tidsstämpeln och alla data fortsätter.

### Hämta senaste batchstatus

Innan du kör nya åtgärder i ETL-verktyget måste du se till att den senaste gruppen slutfördes korrekt. [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) innehåller ett gruppspecifikt alternativ som innehåller information om de relevanta batcharna.

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar**

Nya aktiviteter kan schemaläggas om det tidigare värdet för batchstatus är Slutfört enligt nedan:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Hämta senaste batchstatus med ID

En enskild batchstatus kan hämtas via [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) genom att en GET-förfrågan skickas med `{BATCH_ID}`. `{BATCH_ID}` som används skulle vara samma som det ID som returnerades när gruppen skapades.

**Begäran**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Svar - lyckat**

Följande svar visar&quot;lyckades&quot;:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Svar - Fel**

Om fel uppstår kan&quot;felen&quot; extraheras från svaret och visas som felmeddelanden i ETL-verktyget.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Inkrementella kontra ögonblicksbilddata och händelser jämfört med profiler

Data kan representeras av två matriser enligt följande:

| Inkrementella händelser | Inkrementella profiler |
|-------------------------------|----------------------|
| Ögonblicksbilder (mindre sannolikt) | Snapshot-profiler |

Händelsedata är vanligtvis när det finns indexerade tidsstämpelkolumner i varje rad.

Profildata är vanligtvis när det inte finns någon tidsstämpel i data och varje rad kan identifieras med en primär/sammansatt nyckel.

Stegvisa data är där bara nya/uppdaterade data kommer in i systemet och läggs till i aktuella data i datauppsättningarna.

Snapshot-data är när alla data kommer in i systemet och ersätter vissa eller alla tidigare data i en datauppsättning.

Vid inkrementella händelser bör ETL-verktyget använda tillgängliga datum/skapa-datum för batchenheten. Om du använder en push-tjänst finns inga tillgängliga datum, så verktyget använder batchskapat/uppdaterat datum för markeringssteg. Varje grupp med stegvisa händelser måste bearbetas.

För inkrementella profiler kommer ETL-verktyget att använda skapade/uppdaterade datum för batchentiteten. Vanligtvis krävs varje grupp med inkrementella profildata för att bearbetas.

Det är inte så troligt att händelser för ögonblicksbilder påverkas av datastorleken. Men om detta skulle behövas får ETL-verktyget bara välja den sista gruppen för bearbetning.

När ögonblicksbildsprofiler används måste ETL-verktyget välja den sista gruppen med data som finns i systemet. Men om det är nödvändigt att hålla reda på versionerna av ändringarna måste alla grupper bearbetas. Borttagning av dubbletter i ETL-processen hjälper till att hålla lagringskostnaderna nere.

## Batchrepriser och databearbetning

Batchrepriser och dataombearbetning kan behövas om en klient upptäcker att de data som behandlas i ETL inte har utförts som förväntat under de senaste &#39;n&#39; dagarna, eller om själva källdata inte har varit korrekta.

För att göra detta använder klientens dataadministratörer [!DNL Platform]-gränssnittet för att ta bort de grupper som innehåller skadade data. Därefter kommer ETL sannolikt att behöva köras igen, vilket innebär att korrekta data fylls i igen. Om själva källan innehåller skadade data måste datateknikern/administratören korrigera källbatcherna och importera data igen (antingen till Adobe Experience Platform eller via ETL-anslutningar).

Beroende på vilken typ av data som genereras blir det datateknikerns val att ta bort en enda batch eller alla batchar från vissa datauppsättningar. Data tas bort/arkiveras enligt riktlinjerna för [!DNL Experience Platform].

Det är sannolikt ett scenario där ETL-funktionen för att rensa data är viktig.

När rensningen är klar måste klientadministratörerna konfigurera om Adobe Experience Platform för att starta om bearbetningen för bastjänsterna från den tidpunkt då batcharna tas bort.

## Samtidig batchbearbetning

Efter kundens gottfinnande kan dataadministratörer/ingenjörer besluta att extrahera, omvandla och läsa in data sekventiellt eller samtidigt beroende på egenskaperna för en viss datauppsättning. Detta kommer också att baseras på det användningsfall som klienten har som mål med de omformade data.

Om klienten till exempel är beständig i ett uppdateringsbart beständigt arkiv och händelsesekvensen eller händelseordningen är viktig, kan klienten behöva bearbeta jobb med sekventiella ETL-omvandlingar strikt.

I andra fall kan data i fel ordning bearbetas av program/processer som sorteras internt med en angiven tidsstämpel. I sådana fall kan parallella ETL-omvandlingar vara genomförbara för att förbättra bearbetningstiden.

För källbatchar är den åter beroende av klientinställningar och kundbegränsning. Om källdata kan hämtas upp parallellt utan hänsyn till hur lång raden behöver vara/ordnas, kan omvandlingsprocessen skapa processgrupper med högre grad av parallellitet (optimering baserad på oordningsbearbetning). Men om omvandlingen måste följa tidsstämplar eller ändra prioritetsordning måste schemaläggaren/anropet för dataåtkomst eller ETL-verktyget se till att batchar inte bearbetas i fel ordning där det är möjligt.

## Uppskov

Uppskov är en process där indata ännu inte är tillräckligt fullständiga för att skickas ut till processer längre fram i kedjan, men kan användas i framtiden. Kunderna bestämmer sin individuella tolerans för datarutor för framtida matchning jämfört med kostnaden för bearbetning för att kunna fatta beslut om att ta bort data och bearbeta dem på nytt i nästa omformningskörning, i hopp om att de kan berikas och sys.k. sys.k. vid någon framtida tidpunkt i kvarhållningsfönstret. Denna cykel pågår tills raden behandlas tillräckligt eller den anses vara för gammal för att fortsätta investera. Varje iteration genererar fördröjda data som är en överordnad mängd av alla fördröjda data i tidigare iterationer.

Adobe Experience Platform identifierar för närvarande inte fördröjda data, så klientimplementeringar måste förlita sig på manuella konfigurationer för ETL och datauppsättning för att skapa en annan datauppsättning i [!DNL Platform] som speglar källdatauppsättningen som kan användas för att behålla fördröjda data. I det här fallet liknar fördröjda data ögonblicksbildsdata. Vid varje körning av ETL-omvandlingen kommer källdata att förenas med fördröjda data och skickas för behandling.

## Changelog

| Datum | Åtgärd | Beskrivning |
| ---- | ------ | ----------- |
| 2019-01-19 | Borttagen fältegenskap från datauppsättningar | Datauppsättningar innehöll tidigare en fältegenskap som innehöll en kopia av schemat. Den här funktionen bör inte längre användas. Om egenskapen &quot;fields&quot; hittas bör den ignoreras och &quot;observeradSchema&quot; eller &quot;schemaRef&quot; används i stället. |
| 2019-03-15 | Egenskapen &quot;schemaRef&quot; har lagts till i datamängder | Egenskapen schemaRef för en datauppsättning innehåller en URI som refererar till det XDM-schema som datauppsättningen baseras på och representerar alla möjliga fält som kan användas av datauppsättningen. |
| 2019-03-15 | Alla slutanvändaridentifierare mappas till egenskapen identityMap | &quot;identityMap&quot; är en inkapsling av alla unika identifierare för ett ämne, som CRMID, ECID eller lojalitetsprogram-ID. Den här kartan används av [[!DNL Identity Service]](../identity-service/home.md) för att matcha alla kända och anonyma identiteter för ett motiv och bilda ett enda identitetsdiagram för varje slutanvändare. |
| 2019-05-30 | EOL och Ta bort schemaegenskap från datauppsättningar | Schemaegenskapen för datauppsättningen tillhandahöll en referenslänk till schemat med den borttagna `/xdms`-slutpunkten i [!DNL Catalog] API. Detta har ersatts av en &quot;schemaRef&quot; som innehåller &quot;id&quot;, &quot;version&quot; och &quot;contentType&quot; för schemat enligt den nya [!DNL Schema Registry]-API:n. |
