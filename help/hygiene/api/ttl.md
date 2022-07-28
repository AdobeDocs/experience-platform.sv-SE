---
title: TTL-API-slutpunkt (Time-to-Live) för datauppsättning
description: Med slutpunkten /ttl i Data Hygiene API kan du schemalägga TTL-värden för datamängd i Adobe Experience Platform.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 1%

---

# TTL-slutpunkt (time-to-live) för datauppsättning

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt skölden.

The `/ttl` -slutpunkten i Data Hygiene API gör att du kan schemalägga TTL-protokoll (time-to-live) för datauppsättningar i Adobe Experience Platform.

En TTL för datamängd är bara en tidsfördröjd borttagningsåtgärd. Datauppsättningen är inte skyddad under tiden, så den kan tas bort på annat sätt innan den upphör att gälla.

>[!NOTE]
>
>Även om förfallodatumet anges som en specifik tidpunkt kan det dröja upp till 24 timmar efter det att den faktiska raderingen har påbörjats. När borttagningen har initierats kan det ta upp till sju dagar innan alla spår i datauppsättningen har tagits bort från plattformssystem.

Du kan när som helst innan datauppsättningsborttagningen initieras avbryta TTL-värdet eller ändra dess utlösningstid. När du har avbrutit en TTL kan du öppna den igen genom att ange en ny förfallotid.

När borttagningen av datauppsättningen initieras markeras dess TTL som `executing`och får inte ändras ytterligare. Själva datauppsättningen kan återvinnas i upp till sju dagar, men endast genom en manuell process som initierats via en begäran från Adobe.

## Komma igång

Slutpunkten som används i den här guiden är en del av API:t för datahygien. Läs igenom [översikt](./overview.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som behövs för att kunna anropa ett Experience Platform-API.

## Visa datamängdens TTL {#list}

Du kan visa alla TTL-värden för datauppsättningar för din organisation genom att göra en GET-förfrågan.

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
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar listar de resulterande TTL-värdena. Följande exempel har trunkerats för utrymme.

```json
{
  "results": [
    {
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `results` | Innehåller information om returnerade TTL:er. Mer information om egenskaperna för en TTL-enhet finns i svarsavsnittet för att skapa en [uppslagsanrop](#lookup). |
| `current_page` | Den aktuella sidan med listade resultat. |
| `total_pages` | Det totala antalet sidor i svaret. |
| `total_count` | Det totala antalet TTL-enheter i svaret. |

{style=&quot;table-layout:auto&quot;}

## Slå upp en TTL {#lookup}

Du kan söka efter en TTL för en datamängd via en GET-begäran.

**API-format**

```http
GET /ttl/{TTL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{TTL_ID}` | ID:t för den TTL som du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar information om TTL.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID för datamängden TTL. |
| `datasetId` | ID:t för datauppsättningen som denna TTL gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Aktuell status för TTL. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när TTL senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade TTL-värdet. |

{style=&quot;table-layout:auto&quot;}

## Skapa en TTL {#create}

Du kan lägga till en TTL för en datauppsättning via en POST-förfrågan.

**API-format**

```http
POST /ttl
```

**Begäran**

Följande begäran schemalägger en datauppsättning `5b020a27e7040801dedbf46e` för borttagning i slutet av 2022 (Greenwich Mean Time).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `datasetId` | ID:t för den datauppsättning som du vill schemalägga en TTL för. |
| `expiry` | En ISO 8601-tidsstämpel för när datauppsättningen ska tas bort. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar informationen om TTL, med HTTP-status 200 (OK) om en befintlig TTL uppdaterades, eller 201 (Skapad) om det inte fanns någon befintlig TTL.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID för datamängden TTL. |
| `datasetId` | ID:t för datauppsättningen som denna TTL gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Aktuell status för TTL. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när TTL senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade TTL-värdet. |

{style=&quot;table-layout:auto&quot;}

## Uppdatera en TTL {#update}

Du kan uppdatera en TTL för en datauppsättning via en PUT-begäran.

**API-format**

```http
PUT /ttl/{TTL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{TTL_ID}` | ID:t för den TTL som du vill ändra. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran uppdaterar TTL-värdet för datauppsättningen `5b020a27e7040801dedbf46e` så att den upphör i slutet av 2023 (Greenwich Mean Time).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `expiry` | En ISO 8601-tidsstämpel för när datauppsättningen ska tas bort. |

{style=&quot;table-layout:auto&quot;}

**Svar**

Ett lyckat svar returnerar information om den uppdaterade TTL-listan.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID för datamängden TTL. |
| `datasetId` | ID:t för datauppsättningen som denna TTL gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Aktuell status för TTL. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när TTL senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade TTL-värdet. |

{style=&quot;table-layout:auto&quot;}

## Avbryt en TTL {#delete}

Du kan avbryta en TTL genom att göra en DELETE-begäran.

**API-format**

```http
DELETE /ttl/{TTL_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{TTL_ID}` | ID:t för den TTL som du vill avbryta. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

Följande begäran uppdaterar TTL-värdet för datauppsättningen `5b020a27e7040801dedbf46e` så att den upphör i slutet av 2023 (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar informationen i TTL:n, med dess `status` attribut har nu angetts till `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | ID för datamängden TTL. |
| `datasetId` | ID:t för datauppsättningen som denna TTL gäller för. |
| `imsOrg` | Organisationens ID. |
| `status` | Aktuell status för TTL. |
| `expiry` | Det schemalagda datumet och den schemalagda tidpunkten när datauppsättningen tas bort. |
| `updatedAt` | En tidsstämpel som anger när TTL senast uppdaterades. |
| `updatedBy` | Användaren som senast uppdaterade TTL-värdet. |

{style=&quot;table-layout:auto&quot;}

## Hämta historiken för en TTL

Du kan slå upp historiken för en viss TTL med hjälp av frågeparametern `include=history` i en sökbegäran. Resultatet innehåller information om hur du skapar en TTL-lista, uppdateringar som har tillämpats och om hur den har annullerats eller körts (om tillämpligt).

**API-format**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parameter | Beskrivning |
| --- | --- |
| `{TTL_ID}` | ID:t för den TTL vars historik du vill söka efter. |

{style=&quot;table-layout:auto&quot;}

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar informationen i TTL:n, med en `history` arrayen med information om dess `status`, `expiry`, `updatedAt`och `updatedBy` attribut för var och en av de inspelade uppdateringarna.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | ID för datamängden TTL. |
| `datasetId` | ID:t för datauppsättningen som denna TTL gäller för. |
| `imsOrg` | Organisationens ID. |
| `history` | Visar uppdateringshistoriken för TTL som en array med objekt, där varje objekt innehåller `status`, `expiry`, `updatedAt`och `updatedBy` attribut för TTL vid tidpunkten för uppdateringen. |

{style=&quot;table-layout:auto&quot;}

## Bilaga

### Godkända frågeparametrar {#query-params}

Följande tabell visar de tillgängliga frågeparametrarna när [lista datamängdsTTL](#list):

| Parameter | Beskrivning | Exempel |
| --- | --- | --- |
| `size` | Ett heltal mellan 1 och 100 som anger det maximala antalet TTL-värden som ska returneras. Standardvärdet är 25. | `size=50` |
| `page` | Ett heltal som anger vilken sida med TTL:er som ska returneras. | `page=3` |
| `status` | En kommaavgränsad lista med statusvärden. När svaret inkluderas matchar det TTL-nummer vars aktuella status är bland de listade. | `status=pending,cancelled` |
| `author` | Matchar TTL:er vars `created_by` är en matchning för söksträngen. Om söksträngen börjar med `LIKE` eller `NOT LIKE`behandlas resten som ett SQL-sökmönster. Annars behandlas hela söksträngen som en litteral sträng som exakt måste matcha hela innehållet i en `created_by` fält. | `author=LIKE %john%` |
| `createdDate` | Matchar TTL:er som skapades i 24-timmarsfönstret med början vid angiven tidpunkt.<br><br>Observera att datum utan tid (som `2021-12-07`) representerar datetime i början av den dagen. Således `createdDate=2021-12-07` avser alla TTL-värden som skapades den 7 december 2021, från `00:00:00` via `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Matchar TTL:er som skapades vid eller efter den angivna tiden. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Matchar TTL:er som skapades vid eller före den angivna tiden. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | Gilla `createdDate` / `createdFromDate` / `createdToDate`, men matchar en TTL-s uppdateringstid i stället för skapandetid.<br><br>En TTL betraktas som uppdaterad vid varje redigering, även när den skapas, avbryts eller körs. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Matchar TTL:er som annullerades när som helst i det angivna intervallet. Detta gäller även om TTL-värdet öppnades igen senare (genom att ange ett nytt förfallodatum för samma datauppsättning). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Matchar TTL:er som har slutförts under det angivna intervallet. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Matchar TTL:er som ska köras, eller som redan har körts, under det angivna intervallet. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
