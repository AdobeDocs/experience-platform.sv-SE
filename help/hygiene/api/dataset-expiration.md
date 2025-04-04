---
title: API-slutpunkt för förfallodatum för datauppsättning
description: Med slutpunkten /ttl i Data Hygiene API kan du schemalägga datauppsättningens förfallodatum i Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 0%

---

# Slutpunkt för förfallodatum för datauppsättning

Med slutpunkten `/ttl` i Data Hygiene API kan du schemalägga förfallodatum för datauppsättningar i Adobe Experience Platform.

En datamängds förfallotid är endast en tidsfördröjd borttagningsåtgärd. Datauppsättningen är inte skyddad under tiden, så den kan tas bort på annat sätt innan den upphör att gälla.

>[!NOTE]
>
>Även om förfallodatumet anges som en specifik tidpunkt kan det dröja upp till 24 timmar efter det att den faktiska raderingen har påbörjats. När borttagningen har initierats kan det ta upp till sju dagar innan alla spår i datauppsättningen har tagits bort från Experience Platform-system.

Du kan när som helst innan datauppsättningsborttagningen initieras avbryta förfallotiden eller ändra dess utlösningstid. När du har avbrutit en förfallotid för en datauppsättning kan du öppna den igen genom att ange en ny förfallotid.

När borttagningen av datauppsättningen initieras markeras dess förfallojobb som `executing`, och det kanske inte ändras ytterligare. Själva datauppsättningen kan återvinnas i upp till sju dagar, men endast genom en manuell process som initierats via en begäran från Adobe. När begäran verkställs startar datasjön, identitetstjänsten och kundprofilen i realtid separata processer för att ta bort datauppsättningens innehåll från sina respektive tjänster. När data har tagits bort från alla tre tjänsterna markeras förfallotiden som `completed`.

>[!WARNING]
>
>Om en datauppsättning är inställd på att förfalla måste du manuellt ändra alla dataflöden som kan inhämta data till datauppsättningen så att dina efterföljande arbetsflöden inte påverkas negativt.

Avancerad livscykelhantering för data stöder borttagning av datauppsättningar via datauppsättningens slutpunkt och ID-borttagningar (data på radnivå) med hjälp av primära identiteter via [arbetsorderslutpunkten](./workorder.md). Du kan också hantera [förfallodatum för datauppsättningar](../ui/dataset-expiration.md) och [borttagningar av poster](../ui/record-delete.md) via Experience Platform-gränssnittet. Mer information finns i den länkade dokumentationen.

>[!NOTE]
>
>Datalifecycle stöder inte batchborttagning.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du läsa [API-handboken](./overview.md) för att få information om vilka huvuden som krävs för CRUD-åtgärder, felmeddelanden, Postman-samlingar och hur du läser exempel-API-anrop.

>[!IMPORTANT]
>
>När du anropar data Hygiene API måste du använda huvudet -H `x-sandbox-name: {SANDBOX_NAME}`.

## Visa förfallodatum för datamängd {#list}

Du kan visa alla förfallodatum för datauppsättningar för din organisation genom att göra en GET-förfrågan. Frågeparametrar kan användas för att filtrera svaret för lämpliga resultat.

**API-format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETERS}` | En lista med valfria frågeparametrar, med flera parametrar avgränsade med `&` tecken. Vanliga parametrar är `limit` och `page` för sidnumreringsändamål. En fullständig lista över frågeparametrar som stöds finns i avsnittet [appendix](#query-params). |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar listar de resulterande datauppsättningens förfallotider. Följande exempel har trunkerats för utrymme.

>[!IMPORTANT]
>
>`ttlId` i svaret kallas också `{DATASET_EXPIRATION_ID}`. Båda hänvisar till den unika identifieraren för datauppsättningens förfallodatum.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `total_count` | Antalet datauppsättningsförfallodatum som matchade listanropets parametrar. |
| `results` | Innehåller information om förfallodatum för returnerad datauppsättning. Mer information om egenskaperna för en datamängds förfallotid finns i svarsavsnittet för att ringa ett [uppslagsanrop](#lookup). |

{style="table-layout:auto"}

## Söka efter en förfallotid för en datauppsättning {#lookup}

Om du vill söka efter en förfallotid för en datauppsättning gör du en GET-begäran med antingen `{DATASET_ID}` eller `{DATASET_EXPIRATION_ID}`.

>[!IMPORTANT]
>
>`{DATASET_EXPIRATION_ID}` kallas `ttlId` i svaret. Båda hänvisar till den unika identifieraren för datauppsättningens förfallodatum.

**API-format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars förfallodatum du vill söka efter. |
| `{DATASET_EXPIRATION_ID}` | ID:t för datauppsättningens förfallodatum. |

{style="table-layout:auto"}

**Begäran**

Följande begäran letar upp förfalloinformationen för datauppsättningen `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om datauppsättningens förfallodatum.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `datasetName` | Visningsnamnet för den datauppsättning som förfallodatumet gäller för. |
| `sandboxName` | Namnet på sandlådan som måldatauppsättningen finns under. |
| `imsOrg` | Organisationens ID. |
| `status` | Den aktuella statusen för datauppsättningens utgångsdatum. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när förfallodatumet senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade förfallodatumet. |
| `displayName` | Visningsnamnet för förfallobegäran. |
| `description` | En beskrivning av förfallobegäran. |

{style="table-layout:auto"}

### Förfallotaggar för katalog

När du använder [katalog-API:t](../../catalog/api/getting-started.md) för att söka efter datauppsättningsinformation, kommer den att listas under `tags.adobe/hygiene/ttl` om datauppsättningen har en aktiv förfallotid.

Följande JSON representerar ett trunkerat svar för datauppsättningens information från katalogen, som har ett förfallovärde på `32503680000000`. Taggens värde kodar förfallodatumet som ett heltal i millisekunder sedan början av Unix-epoken.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Skapa en förfallotid för datauppsättning {#create}

För att säkerställa att data tas bort från systemet efter en angiven period schemalägger du en förfallotid för en viss datauppsättning genom att ange datauppsättnings-ID och utgångsdatum och -tid i ISO 8601-format.

Om du vill skapa en förfallotid för en datauppsättning utför du en POST-begäran enligt nedan och anger värdena som anges nedan i nyttolasten.

>[!NOTE]
>
>Om du får ett 404-fel kontrollerar du att begäran inte har några ytterligare snedstreck. Ett avslutande snedstreck kan göra att en POST-begäran misslyckas.

**API-format**

```http
POST /ttl
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Egenskap | Beskrivning |
| --- | --- |
| `datasetId` | **Obligatorisk** ID:t för måldatauppsättningen som du vill schemalägga en förfallotid för. |
| `expiry` | **Obligatoriskt** Ett datum och en tid i ISO 8601-format. Om strängen inte har någon explicit tidszonsförskjutning antas tidszonen vara UTC. Livslängden för data i systemet anges enligt angivet utgångsvärde.<br>Obs!<ul><li>Begäran misslyckas om det redan finns en förfallotid för datauppsättningen.</li><li>Detta datum och denna tid måste vara minst **24 timmar i framtiden**.</li></ul> |
| `displayName` | Ett valfritt visningsnamn för datauppsättningens förfallobegäran. |
| `description` | En valfri beskrivning av förfallobegäran. |

**Svar**

Ett lyckat svar returnerar HTTP 201-status (Skapad) och det nya tillståndet för datauppsättningens förfallodatum.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `datasetName` | Visningsnamnet för den datauppsättning som förfallodatumet gäller för. |
| `sandboxName` | Namnet på sandlådan som måldatauppsättningen finns under. |
| `imsOrg` | Organisationens ID. |
| `status` | Den aktuella statusen för datauppsättningens utgångsdatum. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när förfallodatumet senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade förfallodatumet. |
| `displayName` | Ett visningsnamn för förfallobegäran. |
| `description` | En beskrivning av förfallobegäran. |

HTTP-statusen 400 (Ogiltig begäran) inträffar om det redan finns en förfallotid för datauppsättningen. Ett misslyckat svar returnerar HTTP-statusen 404 (Hittades inte) om det inte finns någon sådan förfallotid (eller om du inte har tillgång till datauppsättningen).

## Uppdatera utgångsdatum för en datauppsättning {#update}

Om du vill uppdatera ett förfallodatum för en datauppsättning använder du en PUT-begäran och `ttlId`. Du kan uppdatera informationen för `displayName`, `description` och/eller `expiry`.

>[!NOTE]
>
>Om du ändrar förfallodatumet och förfallotiden måste det vara minst 24 timmar i framtiden. Denna försening ger dig möjlighet att avbryta eller schemalägga om förfallotiden och undvika oavsiktliga dataförluster.

**API-format**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | ID:t för datauppsättningens förfallodatum som du vill ändra. Obs! Detta kallas `ttlId` i svaret. |

**Begäran**

I följande begäran omdisponeras en datamängds förfallodatum `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` till i slutet av 2024 (Greenwich Mean Time). Om den befintliga datauppsättningens förfallodatum hittas uppdateras den med det nya `expiry`-värdet.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `expiry` | **Obligatoriskt** Ett datum och en tid i ISO 8601-format. Om strängen inte har någon explicit tidszonsförskjutning antas tidszonen vara UTC. Livslängden för data i systemet anges enligt angivet utgångsvärde. Alla tidigare tidsstämplar för förfallodatum för samma datauppsättning ska ersättas med det nya utgångsvärdet som du har angett. Detta datum och denna tid måste vara minst **24 timmar i framtiden**. |
| `displayName` | Ett visningsnamn för förfallobegäran. |
| `description` | En valfri beskrivning av förfallobegäran. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar det nya tillståndet för datauppsättningens förfallodatum och HTTP-statusen 200 (OK) om en tidigare förfallotid uppdaterades.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Den aktuella statusen för datauppsättningens utgångsdatum. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när förfallodatumet senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade förfallodatumet. |

{style="table-layout:auto"}

Ett misslyckat svar returnerar HTTP-statusen 404 (Hittades inte) om det inte finns någon sådan förfallotid för datauppsättningen.

## Avbryt förfallodatum för en datauppsättning {#delete}

Du kan avbryta en förfallotid för en datauppsättning genom att göra en DELETE-begäran.

>[!NOTE]
>
>Det går bara att avbryta datauppsättningsförfallodatum som har statusen `pending`. Om du försöker avbryta ett förfallodatum som har körts eller som redan har avbrutits returneras ett HTTP 404-fel.

**API-format**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPIRATION_ID}` | `ttlId` av datauppsättningens förfallodatum som du vill avbryta. |

{style="table-layout:auto"}

**Begäran**

Följande begäran avbryter en förfallotid för en datauppsättning med ID `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 204 (inget innehåll) och förfallofilens `status`-attribut är inställt på `cancelled`.

## Bilaga

### Godkända frågeparametrar {#query-params}

I följande tabell visas de tillgängliga frågeparametrarna när [en lista över datauppsättningens förfallotider](#list) visas:

>[!NOTE]
>
>Parametrarna `description`, `displayName` och `datasetName` innehåller alla möjlighet att söka efter LIKE-värden. Det innebär att du kan hitta schemalagda datauppsättningsförfallotider med namnet&quot;Name123&quot;,&quot;Name183&quot;,&quot;DisplayName1234&quot; genom att söka efter strängen&quot;Name1&quot;.

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `author` | Använd frågeparametern `author` för att hitta den person som senast uppdaterade utgångsdatumet för datauppsättningen. Om inga uppdateringar har gjorts sedan den skapades matchar detta den ursprungliga skaparen av förfallodatumet. Den här parametern matchar förfallodatum där fältet `created_by` motsvarar söksträngen.<br>Om söksträngen börjar med `LIKE` eller `NOT LIKE` behandlas resten som ett SQL-sökmönster. Annars behandlas hela söksträngen som en literal sträng som exakt måste matcha hela innehållet i ett `created_by`-fält. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Matchar förfallodatum som gäller för en viss datauppsättning. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Matchar förfallodatum vars datauppsättningsnamn innehåller den angivna söksträngen. Matchen är inte skiftlägeskänslig. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Matchar förfallodatum vars visningsnamn innehåller den angivna söksträngen. Matchen är inte skiftlägeskänslig. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtrerar resultat baserat på ett exakt körningsdatum, ett körningsdatum eller ett startdatum för körning. De används för att hämta data eller poster som är kopplade till körningen av en åtgärd på ett visst datum, före ett visst datum eller efter ett visst datum. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Matchar utgångsdatum som inträffade i det 24-timmarsfönstret för det angivna datumet. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Matchar förfallodatum som ska verkställas, eller som redan har körts, under det angivna intervallet. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Ett heltal mellan 1 och 100 som anger det maximala antalet förfallodatum som ska returneras. Standardvärdet är 25. | `limit=50` |
| `orderBy` | Frågeparametern `orderBy` anger sorteringsordningen för resultaten som returneras av API:t. Använd den för att ordna data baserat på ett eller flera fält, antingen i stigande (ASC) eller fallande (DESC) ordning. Använd prefixet + eller - för att beteckna ASC respektive DESC. Följande värden accepteras: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Matchar datamängdernas förfallodatum vars organisations-ID matchar parameterns. Det här värdet är som standard det för `x-gw-ims-org-id`-huvudena och ignoreras om inte begäran tillhandahåller en tjänsttoken. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Ett heltal som anger vilken sida med förfallodatum som ska returneras. | `page=3` |
| `sandboxName` | Matchar datauppsättningens förfallodatum vars sandlådenamn exakt matchar argumentet. Standardvärdet är sandlådenamnet i begärans `x-sandbox-name`-huvud. Använd `sandboxName=*` om du vill inkludera förfallodatum för datauppsättning från alla sandlådor. | `sandboxName=dev1` |
| `search` | Matchar utgångsdatum där den angivna strängen är en exakt matchning för förfallodatum-ID, eller är **innesluten** i något av dessa fält:<br><ul><li>författare</li><li>visningsnamn</li><li>description</li><li>visningsnamn</li><li>datauppsättningsnamn</li></ul> | `search=TESTING` |
| `status` | En kommaavgränsad lista med statusvärden. När svaret inkluderas matchar det utgångsdatum för datauppsättningen vars aktuella status är bland de som visas. | `status=pending,cancelled` |
| `ttlId` | Matchar förfallobegäran med angivet ID. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Matchar utgångsdatum som uppdaterades i det 24-timmarsfönstret för det angivna datumet. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Matchar utgångsdatum som uppdaterades i 24-timmarsfönstret med början vid angiven tidpunkt.<br><br>En förfallotid anses vara uppdaterad vid varje redigering, inklusive när den skapas, avbryts eller körs. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

