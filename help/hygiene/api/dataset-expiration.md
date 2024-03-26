---
title: API-slutpunkt för förfallodatum för datauppsättning
description: Med slutpunkten /ttl i Data Hygiene API kan du schemalägga datauppsättningens förfallodatum i Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 04d49282d60b2e886a6d2dae281b98b60e6ce9b3
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# Slutpunkt för förfallodatum för datauppsättning

The `/ttl` kan du schemalägga förfallodatum för datauppsättningar i Adobe Experience Platform.

En datamängds förfallotid är endast en tidsfördröjd borttagningsåtgärd. Datauppsättningen är inte skyddad under tiden, så den kan tas bort på annat sätt innan den upphör att gälla.

>[!NOTE]
>
>Även om förfallodatumet anges som en specifik tidpunkt kan det dröja upp till 24 timmar efter det att den faktiska raderingen har påbörjats. När borttagningen har initierats kan det ta upp till sju dagar innan alla spår i datauppsättningen har tagits bort från plattformssystem.

Du kan när som helst innan datauppsättningsborttagningen initieras avbryta förfallotiden eller ändra dess utlösningstid. När du har avbrutit en förfallotid för en datauppsättning kan du öppna den igen genom att ange en ny förfallotid.

När borttagningen av datauppsättningen initieras markeras dess förfallojobb som `executing`och får inte ändras ytterligare. Själva datauppsättningen kan återvinnas i upp till sju dagar, men endast genom en manuell process som initierats via en begäran från Adobe. När begäran verkställs startar datasjön, identitetstjänsten och kundprofilen i realtid separata processer för att ta bort datauppsättningens innehåll från sina respektive tjänster. När data har tagits bort från alla tre tjänsterna är förfallodatumet markerat som `executed`.

>[!WARNING]
>
>Om en datauppsättning är inställd på att förfalla måste du manuellt ändra alla dataflöden som kan inhämta data till datauppsättningen så att dina efterföljande arbetsflöden inte påverkas negativt.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Innan du fortsätter bör du granska [API-guide](./overview.md) för information om obligatoriska rubriker för CRUD-åtgärder, felmeddelanden, Postman-samlingar och hur du läser exempel-API-anrop.

>[!IMPORTANT]
>
>När du anropar data Hygiene API måste du använda -H `x-sandbox-name: {SANDBOX_NAME}` header.

## Visa förfallodatum för datamängd {#list}

Du kan visa alla förfallodatum för datauppsättningar för din organisation genom att göra en GET-förfrågan. Frågeparametrar kan användas för att filtrera svaret för lämpliga resultat.

**API-format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETERS}` | En lista med valfria frågeparametrar, med flera parametrar avgränsade med `&` tecken. Vanliga parametrar inkluderar `limit` och `page` för sidnumrering. En fullständig lista över frågeparametrar som stöds finns i [appendix-avsnitt](#query-params). |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar listar de resulterande datauppsättningens förfallotider. Följande exempel har trunkerats för utrymme.

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
| `totalRecords` | Antalet datauppsättningsförfallodatum som matchade listanropets parametrar. |
| `ttlDetails` | Innehåller information om förfallodatum för returnerad datauppsättning. Mer information om egenskaperna för en datamängds förfallodatum finns i svarsavsnittet för att skapa en [uppslagsanrop](#lookup). |

{style="table-layout:auto"}

## Söka efter en förfallotid för en datauppsättning {#lookup}

Om du vill söka efter en förfallotid för en datauppsättning gör du en GET-förfrågan med antingen `datasetId` eller `ttlId`.

**API-format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars förfallodatum du vill söka efter. |
| `{TTL_ID}` | ID:t för datauppsättningens förfallodatum. |

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

När du använder [Katalog-API](../../catalog/api/getting-started.md) om du vill söka efter datauppsättningsinformation, om datauppsättningen har en aktiv förfallotid, visas den under `tags.adobe/hygiene/ttl`.

Följande JSON representerar ett trunkerat svar för datauppsättningens information från Catalog, som har ett förfallovärde på `32503680000000`. Taggens värde kodar förfallodatumet som ett heltal i millisekunder sedan början av Unix-epoken.

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

Om du vill skapa en förfallotid för en datauppsättning utför du en begäran om POST enligt nedan och anger de värden som anges nedan i nyttolasten.

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
| `datasetId` | **Obligatoriskt** ID:t för måldatauppsättningen som du vill schemalägga en förfallotid för. |
| `expiry` | **Obligatoriskt** Ett datum och en tid i ISO 8601-format. Om strängen inte har någon explicit tidszonsförskjutning antas tidszonen vara UTC. Livslängden för data i systemet anges enligt angivet utgångsvärde.<br>Obs!<ul><li>Begäran misslyckas om det redan finns en förfallotid för datauppsättningen.</li><li>Det här datumet och den här tiden måste vara minst **24 timmar i framtiden**.</li></ul> |
| `displayName` | Ett valfritt visningsnamn för datauppsättningens förfallobegäran. |
| `description` | En valfri beskrivning av förfallobegäran. |

**Svar**

Ett lyckat svar returnerar HTTP 201-status (Skapad) och det nya tillståndet för datauppsättningens förfallodatum, om det inte fanns någon tidigare förfallotid för datauppsättningen.

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

HTTP-statusen 400 (Ogiltig begäran) inträffar om det redan finns en förfallotid för datauppsättningen. Ett misslyckat svar returnerar HTTP-statusen 404 (Hittades inte) om det inte finns någon sådan förfallotid (eller om du inte har tillgång till den).

## Uppdatera utgångsdatum för en datauppsättning {#update}

Om du vill uppdatera ett förfallodatum för en datauppsättning använder du en PUT-begäran och `ttlId`. Du kan uppdatera `displayName`, `description`och/eller `expiry` information.

>[!NOTE]
>
>Om du ändrar förfallodatumet och förfallotiden måste det vara minst 24 timmar i framtiden. Denna försening ger dig möjlighet att avbryta eller schemalägga om förfallotiden och undvika oavsiktliga dataförluster.

**API-format**

```http
PUT /ttl/{TTL_ID}
```

<!-- We should be avoiding usage of TTL, Can I change that to {EXPIRY_ID} or {EXPIRATION_ID} instead? -->

| Parameter | Beskrivning |
| --- | --- |
| `{TTL_ID}` | ID:t för datauppsättningens förfallodatum som du vill ändra. |

**Begäran**

Följande begäran ändrar förfallodatum för en datauppsättning `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` i slutet av 2024 (GMT). Om den befintliga datauppsättningens förfallodatum hittas uppdateras den med den nya `expiry` värde.

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
| `expiry` | **Obligatoriskt** Ett datum och en tid i ISO 8601-format. Om strängen inte har någon explicit tidszonsförskjutning antas tidszonen vara UTC. Livslängden för data i systemet anges enligt angivet utgångsvärde. Alla tidigare tidsstämplar för förfallodatum för samma datauppsättning ersätts med det nya utgångsvärdet som du har angett. Det här datumet och den här tiden måste vara minst **24 timmar i framtiden**. |
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
>Endast förfallodatum för datauppsättning som har statusen `pending` kan avbrytas. Om du försöker avbryta ett förfallodatum som har körts eller som redan har avbrutits returneras ett HTTP 404-fel.

**API-format**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{EXPIRATION_ID}` | The `ttlId` av datauppsättningens förfallodatum som du vill avbryta. |

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

Ett godkänt svar returnerar HTTP-status 204 (inget innehåll) och förfallodatumet `status` attribute is set to `cancelled`.

## Hämta förfallostatushistoriken för en datauppsättning {#retrieve-expiration-history}

Du kan slå upp förfallostatushistoriken för en viss datauppsättning med hjälp av frågeparametern `include=history` i en sökbegäran. Resultatet innehåller information om hur datauppsättningens förfallodatum skapas, vilka uppdateringar som har gjorts och hur den avbryts eller körs (om tillämpligt). Du kan också använda `ttlId` av datauppsättningens förfallodatum.

**API-format**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars förfallohistorik du vill söka efter. |
| `{TTL_ID}` | ID:t för datauppsättningens förfallodatum. |

{style="table-layout:auto"}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett svar returnerar information om datauppsättningens förfallodatum, med en `history` arrayen med information om dess `status`, `expiry`, `updatedAt`och `updatedBy` attribut för var och en av de registrerade uppdateringarna.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `datasetName` | Visningsnamnet för den datauppsättning som förfallodatumet gäller för. |
| `sandboxName` | Namnet på sandlådan som måldatauppsättningen finns under. |
| `displayName` | Visningsnamnet för förfallobegäran. |
| `description` | En beskrivning av förfallobegäran. |
| `imsOrg` | Organisationens ID. |
| `history` | Visar historiken för uppdateringar för förfallodatumet som en array med objekt, där varje objekt innehåller `status`, `expiry`, `updatedAt`och `updatedBy` attribut för förfallodatum vid tidpunkten för uppdateringen. |

{style="table-layout:auto"}

## Bilaga

### Godkända frågeparametrar {#query-params}

Följande tabell visar de tillgängliga frågeparametrarna när [ange förfallodatum för datauppsättning](#list):

>[!NOTE]
>
>The `description`, `displayName`och `datasetName` alla parametrar kan användas för att söka efter LIKE-värden. Det innebär att du kan hitta schemalagda datauppsättningsförfallotider med namnet&quot;Name123&quot;,&quot;Name183&quot;,&quot;DisplayName1234&quot; genom att söka efter strängen&quot;Name1&quot;.

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `author` | Matchar förfallodatum vars `created_by` är en matchning för söksträngen. Om söksträngen börjar med `LIKE` eller `NOT LIKE`behandlas resten som ett SQL-sökmönster. Annars behandlas hela söksträngen som en litteral sträng som exakt måste matcha hela innehållet i en `created_by` fält. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Matchar förfallodatum som annullerades när som helst i det angivna intervallet. Detta gäller även om utgångsdatumet öppnades igen senare (genom att ange ett nytt förfallodatum för samma datauppsättning). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Matchar förfallotider som har slutförts under det angivna intervallet. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Matchar utgångsdatum som skapades i 24-timmarsfönstret med början vid angiven tidpunkt.<br><br>Observera att datum utan tid (som `2021-12-07`) representerar datetime i början av den dagen. Således `createdDate=2021-12-07` avser alla förfallodatum som skapades den 7 december 2021, från `00:00:00` via `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Matchar utgångsdatum som skapades vid eller efter den angivna tiden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Matchar utgångsdatum som skapades vid eller före angiven tid. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Matchar förfallodatum som gäller för en viss datauppsättning. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Matchar förfallodatum vars datauppsättningsnamn innehåller den angivna söksträngen. Matchen är inte skiftlägeskänslig. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Matchar förfallodatum vars visningsnamn innehåller den angivna söksträngen. Matchen är inte skiftlägeskänslig. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Filtrerar resultat baserat på ett exakt körningsdatum, ett körningsdatum eller ett startdatum för körning. De används för att hämta data eller poster som är kopplade till körningen av en åtgärd på ett visst datum, före ett visst datum eller efter ett visst datum. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Matchar förfallodatum som ska verkställas, eller som redan har körts, under det angivna intervallet. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Ett heltal mellan 1 och 100 som anger det maximala antalet förfallodatum som ska returneras. Standardvärdet är 25. | `limit=50` |
| `orderBy` | The `orderBy` frågeparametern anger sorteringsordningen för de resultat som returneras av API:t. Använd den för att ordna data baserat på ett eller flera fält, antingen i stigande (ASC) eller fallande (DESC) ordning. Använd prefixet + eller - för att beteckna ASC respektive DESC. Följande värden accepteras: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Matchar datamängdernas förfallodatum vars organisations-ID matchar parameterns. Standardvärdet är `x-gw-ims-org-id` huvuden och ignoreras såvida inte begäran tillhandahåller en tjänsttoken. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Ett heltal som anger vilken sida med förfallodatum som ska returneras. | `page=3` |
| `sandboxName` | Matchar datauppsättningens förfallodatum vars sandlådenamn exakt matchar argumentet. Standardvärdet är sandlådenamnet i begäran `x-sandbox-name` header. Använd `sandboxName=*` om du vill inkludera förfallodatum för datauppsättningar från alla sandlådor. | `sandboxName=dev1` |
| `search` | Matchar utgångsdatum där den angivna strängen är en exakt matchning för förfallodatum-ID:t, eller är **innesluten** i något av dessa fält:<br><ul><li>författare</li><li>visningsnamn</li><li>description</li><li>visningsnamn</li><li>datauppsättningsnamn</li></ul> | `search=TESTING` |
| `status` | En kommaavgränsad lista med statusvärden. När svaret inkluderas matchar det utgångsdatum för datauppsättningen vars aktuella status är bland de som visas. | `status=pending,cancelled` |
| `ttlId` | Matchar förfallobegäran med angivet ID. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Gilla `createdDate` / `createdFromDate` / `createdToDate`, men matchar en datamängds uppdateringstid i stället för skapandetid.<br><br>En förfallotid anses vara uppdaterad för varje redigering, inklusive när den skapas, avbryts eller körs. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

