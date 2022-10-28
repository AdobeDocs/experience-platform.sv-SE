---
title: API-slutpunkt för förfallodatum för datauppsättning
description: Med slutpunkten /ttl i Data Hygiene API kan du schemalägga datauppsättningens förfallodatum i Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# Slutpunkt för förfallodatum för datauppsättning

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt Adobe Healthcare Shield.

The `/ttl` -slutpunkten i Data Hygiene API gör att du kan schemalägga förfallodatum för datauppsättningar i Adobe Experience Platform.

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

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Läs igenom [översikt](./overview.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Visa förfallodatum för datauppsättning {#list}

Du kan visa alla förfallodatum för datauppsättningar för din organisation genom att göra en GET-förfrågan.

**API-format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETERS}` | En lista med valfria frågeparametrar, med flera parametrar avgränsade med `&` tecken. Vanliga parametrar inkluderar `size` och `page` för sidnumrering. En fullständig lista över frågeparametrar som stöds finns i [appendix-avsnitt](#query-params). |

{style=&quot;table-layout:auto&quot;}

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
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `totalRecords` | Antalet datauppsättningsförfallodatum som matchade listanropets parametrar. |
| `ttlDetails` | Innehåller information om förfallodatum för returnerad datauppsättning. Mer information om egenskaperna för en datamängds förfallodatum finns i svarsavsnittet för att skapa en [uppslagsanrop](#lookup). |

{style=&quot;table-layout:auto&quot;}

## Söka efter en förfallotid för en datauppsättning {#lookup}

Du kan söka efter en förfallotid för en datauppsättning via en GET-begäran.

**API-format**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars förfallodatum du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

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
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Den aktuella statusen för datauppsättningens förfallodatum. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när förfallodatumet senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade förfallodatumet. |
| `displayName` | Visningsnamnet för förfallobegäran. |
| `description` | En beskrivning av förfallobegäran. |

{style=&quot;table-layout:auto&quot;}

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

## Skapa eller uppdatera en förfallotid för en datauppsättning {#create-or-update}

Du kan skapa eller uppdatera ett förfallodatum för en datauppsättning via en PUT-begäran.

**API-format**

```http
PUT /ttl/{DATASET_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning som du vill schemalägga en förfallotid för. |

**Begäran**

Följande begäran schemalägger en datauppsättning `5b020a27e7040801dedbf46e` för borttagning i slutet av 2022 (Greenwich Mean Time). Om det inte finns något förfallodatum för datauppsättningen skapas ett nytt förfallodatum. Om datauppsättningen redan har en väntande förfallotid uppdateras den med den nya `expiry` värde.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `expiry` | En ISO 8601-tidsstämpel för när datauppsättningen ska tas bort. |
| `displayName` | Ett visningsnamn för förfallobegäran. |
| `description` | En valfri beskrivning av förfallobegäran. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om datauppsättningens förfallodatum, med HTTP-status 200 (OK) om en befintlig förfallotid uppdaterades, eller 201 (Skapad) om det inte fanns någon tidigare förfallotid.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Den aktuella statusen för datauppsättningens förfallodatum. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när förfallodatumet senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade förfallodatumet. |

{style=&quot;table-layout:auto&quot;}

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
| `{EXPIRATION_ID}` | The `workorderId` av datauppsättningens förfallodatum som du vill avbryta. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran avbryter en förfallotid för en datauppsättning med ID `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar HTTP-status 204 (inget innehåll) och förfallodatumet `status` attribute is set to `cancelled`.

## Hämta förfallostatushistoriken för en datauppsättning

Du kan slå upp förfallostatushistoriken för en viss datauppsättning med hjälp av frågeparametern `include=history` i en sökbegäran. Resultatet innehåller information om hur datauppsättningens förfallodatum skapas, om uppdateringar har tillämpats och om hur den har annullerats eller körts (om tillämpligt).

**API-format**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_ID}` | ID:t för den datauppsättning vars förfallohistorik du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

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

Ett svar returnerar information om datauppsättningens förfallodatum, med en `history` arrayen med information om dess `status`, `expiry`, `updatedAt`och `updatedBy` attribut för var och en av de inspelade uppdateringarna.

```json
{
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `workorderId` | ID:t för datauppsättningens förfallodatum. |
| `datasetId` | ID:t för datauppsättningen som utgångsdatumet gäller för. |
| `datasetName` | Visningsnamnet för den datauppsättning som förfallodatumet gäller för. |
| `sandboxName` | Namnet på sandlådan som måldatauppsättningen finns under. |
| `displayName` | Visningsnamnet för förfallobegäran. |
| `description` | En beskrivning av förfallobegäran. |
| `imsOrg` | Organisationens ID. |
| `history` | Visar historiken för uppdateringar för förfallodatumet som en array med objekt, där varje objekt innehåller `status`, `expiry`, `updatedAt`och `updatedBy` attribut för förfallodatum vid tidpunkten för uppdateringen. |

{style=&quot;table-layout:auto&quot;}

## Bilaga

### Godkända frågeparametrar {#query-params}

Följande tabell visar de tillgängliga frågeparametrarna när [ange förfallodatum för datauppsättning](#list):

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `size` | Ett heltal mellan 1 och 100 som anger det maximala antalet förfallodatum som ska returneras. Standardvärdet är 25. | `size=50` |
| `page` | Ett heltal som anger vilken sida med förfallodatum som ska returneras. | `page=3` |
| `orgId` | Matchar datamängdernas förfallodatum vars organisations-ID matchar parameterns. Standardvärdet är `x-gw-ims-org-id` huvuden och ignoreras såvida inte begäran tillhandahåller en tjänsttoken. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | En kommaavgränsad lista med statusvärden. När svaret inkluderas matchar det utgångsdatum för datauppsättningen vars aktuella status är bland de som visas. | `status=pending,cancelled` |
| `author` | Matchar förfallodatum vars `created_by` är en matchning för söksträngen. Om söksträngen börjar med `LIKE` eller `NOT LIKE`behandlas resten som ett SQL-sökmönster. Annars behandlas hela söksträngen som en litteral sträng som exakt måste matcha hela innehållet i en `created_by` fält. | `author=LIKE %john%` |
| `sandboxName` | Matchar datauppsättningens förfallodatum vars sandlådenamn exakt matchar argumentet. Standardvärdet är sandlådenamnet i begäran `x-sandbox-name` header. Använd `sandboxName=*` om du vill inkludera förfallodatum för datauppsättningar från alla sandlådor. | `sandboxName=dev1` |
| `datasetId` | Matchar förfallodatum som gäller för en viss datauppsättning. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Matchar utgångsdatum som skapades i 24-timmarsfönstret med början vid angiven tidpunkt.<br><br>Observera att datum utan tid (som `2021-12-07`) representerar datetime i början av den dagen. Således `createdDate=2021-12-07` avser alla förfallodatum som skapades den 7 december 2021, från `00:00:00` via `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Matchar utgångsdatum som skapades vid eller efter den angivna tiden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Matchar utgångsdatum som skapades vid eller före angiven tid. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Gilla `createdDate` / `createdFromDate` / `createdToDate`, men matchar en datamängds uppdateringstid i stället för skapandetid.<br><br>En förfallotid anses vara uppdaterad för varje redigering, inklusive när den skapas, avbryts eller körs. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Matchar förfallodatum som annullerades när som helst i det angivna intervallet. Detta gäller även om utgångsdatumet öppnades igen senare (genom att ange ett nytt förfallodatum för samma datauppsättning). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Matchar förfallotider som har slutförts under det angivna intervallet. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Matchar förfallodatum som ska verkställas, eller som redan har körts, under det angivna intervallet. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
