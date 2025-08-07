---
title: API-slutpunkt för förfallodatum för datauppsättning
description: Med slutpunkten /ttl i Data Hygiene API kan du schemalägga datauppsättningens förfallodatum i Adobe Experience Platform.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 0%

---

# Slutpunkt för förfallodatum för datauppsättning

Använd `/ttl`-slutpunkten i Data Hygiene API för att schemalägga när datauppsättningar i Adobe Experience Platform ska tas bort.

En datamängds förfallodatum är en fördröjd borttagningsåtgärd. Datauppsättningen är inte skyddad i mellantiden och kan tas bort på annat sätt innan dess planerade förfallodatum.

>[!NOTE]
>
>Även om förfallodatumet anges som en specifik tidpunkt kan det dröja upp till 24 timmar efter det att den faktiska raderingen har påbörjats. När borttagningen har initierats kan det ta upp till sju dagar innan alla spår i datauppsättningen har tagits bort från Experience Platform-system.

Innan borttagningen börjar kan du avbryta förfallodatumet eller ändra den schemalagda tiden. Ange ett nytt förfallodatum om du vill öppna ett annullerat förfallodatum.

När borttagningen påbörjas markeras förfallojobbet som `executing` och kan inte längre ändras. Datauppsättningen kan återvinnas i upp till sju dagar, men endast genom en manuell begäran från Adobe. Under borttagningen tar datasjön, identitetstjänsten och kundprofilen i realtid bort datauppsättningsinnehållet separat. När borttagningen är klar markeras förfallotiden som `completed`.

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

Du kan visa alla datauppsättningsförfallotider som har konfigurerats för din organisation genom att göra en GET-begäran till slutpunkten `/ttl`.

Filtrera resultat med frågeparametrar för att returnera endast förfallotider som uppfyller dina villkor. Varje resultat innehåller status- och konfigurationsinformation för varje datamängds förfallodatum.

**API-format**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
| --- | --- |
| `{QUERY_PARAMETERS}` | En lista med valfria frågeparametrar, med flera parametrar avgränsade med `&` tecken. Vanliga parametrar är `limit` och `page` för sidnumreringsändamål. En fullständig lista över frågeparametrar som stöds finns i avsnittet [appendix](#query-params) med en fullständig lista över frågeparametrar som stöds. De vanligaste parametrarna finns nedan och i bilagan. |
| `author` | Filtrera efter den användare som senast uppdaterade eller skapade datauppsättningens förfallodatum. Stöder SQL-liknande mönster (till exempel `LIKE %john%`). |
| `datasetId` | Filtrera förfallotider med ett specifikt datauppsättnings-ID. |
| `datasetName` | Ett skiftlägesokänsligt filter för datauppsättningsnamn matchar. |
| `status` | Filtrera efter en kommaavgränsad lista med status: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filtrera efter förfallodatum med ett visst förfallodatum. |
| `limit` | Ange det maximala antalet resultat som ska returneras (1-100, standard: 25). |
| `page` | Sidnumreringen resulterar med ett nollbaserat index (standardsidstorlek: 50, max: 100). |

{style="table-layout:auto"}

**Begäran**

Följande begäran hämtar alla datauppsättningsförfallodatum som har uppdaterats före 1 augusti 2021 och senast uppdaterats av en användare vars namn matchar &quot;Jane Doe&quot;.

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `results` | En matris med konfigurationer för förfallodatum för datauppsättning. |
| `ttlId` | Den unika identifieraren för datauppsättningens förfallokonfiguration. |
| `datasetId` | Den unika identifieraren för den datauppsättning som är associerad med den här konfigurationen. |
| `datasetName` | Datauppsättningens namn. |
| `sandboxName` | Sandlådan där den här datauppsättningens förfallodatum är konfigurerad. |
| `displayName` | Ett läsbart namn för förfallokonfigurationen. |
| `description` | En beskrivning av förfallokonfigurationen. |
| `imsOrg` | Din unika organisations-ID. |
| `status` | Förfallotidens aktuella status. Ett av: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Det schemalagda förfallodatumet och förfallotiden (ISO 8601-format). |
| `updatedAt` | Tidsstämpeln för den senaste uppdateringen av den här konfigurationen. |
| `updatedBy` | Identifieraren och e-postadressen till den användare eller tjänst som senast uppdaterade konfigurationen. |
| `current_page` | Index för den aktuella resultatsidan (nollbaserad). |
| `total_pages` | Det totala antalet tillgängliga resultatsidor. |
| `total_count` | Det totala antalet returnerade konfigurationsposter för förfallodatum för datauppsättning. |

{style="table-layout:auto"}

## Söka efter en förfallotid för en datauppsättning {#lookup}

Hämta information om en viss förfallokonfiguration för datauppsättning genom att göra en GET-begäran med antingen datauppsättningens förfallodatum-ID eller datauppsättnings-ID som sökvägsparameter.

>[!IMPORTANT]
>
>Du kan antingen ange ett förfallodatum-ID för datauppsättning (till exempel `SD-xxxxxx-xxxx`) eller ett datauppsättnings-ID i sökvägen. `ttlId` i svaret är den unika identifieraren för datauppsättningens förfallodatum.

**API-format**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parameter | Beskrivning |
| --- | --- |
| `{ID}` | Den unika identifieraren för datauppsättningens förfallokonfiguration. Du kan antingen ange ett förfallodatum-ID för datauppsättningen eller ett datauppsättnings-ID. |
| `include` | (Valfritt) Om värdet är `history` innehåller svaret en `history`-array med ändringshändelser för konfigurationen. |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | Den unika identifieraren för datauppsättningens förfallokonfiguration. |
| `datasetId` | Den unika identifieraren för datauppsättningen. |
| `datasetName` | Datauppsättningens namn. |
| `sandboxName` | Sandlådan där datauppsättningens förfallodatum konfigureras. |
| `displayName` | Ett läsbart namn för datauppsättningens förfallokonfiguration. |
| `description` | En beskrivning av datauppsättningens förfallokonfiguration. |
| `imsOrg` | Din unika organisationsidentifierare som är associerad med den här konfigurationen. |
| `status` | Den aktuella statusen för datauppsättningens förfallokonfiguration.<br>En av: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Den schemalagda förfallotidsstämpeln för datauppsättningen (ISO 8601-format). |
| `updatedAt` | Tidsstämpel för den senaste uppdateringen. |
| `updatedBy` | Identifieraren och e-postadressen för den användare eller tjänst som senast uppdaterade datauppsättningens förfallodatum. |

{style="table-layout:auto"}

### Förfallotaggar för katalog

När du använder [katalog-API:t](../../catalog/api/getting-started.md) för att söka efter datauppsättningsinformation, kommer den att listas under `tags.adobe/hygiene/ttl` om datauppsättningen har en aktiv förfallotid.

Följande JSON visar ett trunkerat Catalog API-svar för en datauppsättning med ett förfallovärde på `32503680000000`. Taggen kodar förfallodatumet som antalet millisekunder sedan Unix-epoken.

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

Skapa en ny utgångskonfiguration för datauppsättningar som definierar när en datauppsättning upphör att gälla och kan tas bort.\
Ange datauppsättnings-ID, utgångsdatum eller datum-tid (i ISO 8601-format), ett visningsnamn och (eventuellt) en beskrivning.

>[!NOTE]
>
>Utgångsvärdet kan vara ett datum (ÅÅÅÅ-MM-DD) eller ett datum och en tid (ÅÅÅÅ-MM-DDTHH:MM:SSZ). Om du bara anger ett datum används midnatt UTC (00:00:00Z) den dagen. Utgångsdatumet måste vara minst 24 timmar i framtiden.

Om du vill skapa en förfallotid för en datauppsättning skickar du en POST-begäran enligt nedan.

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `datasetId` | **Krävs.** Den unika identifieraren för datauppsättningen som ska tillämpa förfallotiden. |
| `expiry` | **Krävs.** Utgångsdatum och -tid i ISO 8601-format. Detta definierar livslängden för data i systemet. Om bara ett datum anges blir standardvärdet midnatt UTC (00:00:00Z). Utgångsdatumet **måste vara minst 24 timmar i framtiden**. <br>**OBS**:<ul><li>Begäran misslyckas om det redan finns en förfallotid för datauppsättningen.</li></ul> |
| `displayName` | **Krävs.** Ett läsbart namn för datauppsättningens förfallokonfiguration. |
| `description` | En valfri beskrivning av datauppsättningens förfallokonfiguration. |

**Svar**

Ett lyckat svar returnerar en HTTP 201-status (skapad) och den nya konfigurationen för förfallodatum.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | Den unika identifieraren för den skapade datauppsättningens förfallokonfiguration. |
| `datasetId` | Den unika identifieraren för datauppsättningen. |
| `datasetName` | Datauppsättningens namn. |
| `sandboxName` | Sandlådan där den här datauppsättningens förfallodatum är konfigurerad. |
| `displayName` | Visningsnamnet för datauppsättningens förfallokonfiguration. |
| `description` | En beskrivning av datauppsättningens förfallokonfiguration. |
| `imsOrg` | Din unika organisationsidentifierare som är associerad med den här konfigurationen. |
| `status` | Den aktuella statusen för datauppsättningens förfallokonfiguration.<br>En av: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Den schemalagda förfallotidsstämpeln för datauppsättningen. |
| `updatedAt` | Tidsstämpeln för den senaste uppdateringen. |
| `updatedBy` | Identifieraren och e-postadressen för den användare eller tjänst som senast uppdaterade förfallokonfigurationen för datauppsättningen. |

HTTP-statusen 400 (Ogiltig begäran) inträffar om det redan finns en förfallotid för datauppsättningen. HTTP-statusen 404 (Hittades inte) inträffar om det inte finns någon sådan datauppsättning eller om du inte har tillgång till datauppsättningen.

## Uppdatera en förfallokonfiguration för datauppsättning {#update}

Om du vill uppdatera en befintlig förfallokonfiguration för datauppsättning gör du en PUT-begäran till `/ttl/DATASET_EXPIRATION_ID`. Du kan bara uppdatera fälten `displayName`, `description` och `expiry` för konfigurationen. Uppdateringar tillåts bara när förfallostatusen är `pending`.

>[!NOTE]
>
>Fältet `expiry` accepterar ett datum (ÅÅÅÅ-MM-DD) eller datum och tid (ÅÅÅÅ-MM-DDTHH:MM:SSZ). Om endast ett datum anges används midnatt UTC (00:00:00Z) den dagen. Utgångsdatumet **måste vara minst 24 timmar i framtiden**.

**API-format**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Den unika identifieraren för datauppsättningens förfallokonfiguration. **Obs!** Det här kallas `ttlId` i svaret. |

**Begäran**

Följande begäran uppdaterar förfallodatum, visningsnamn och beskrivning för datauppsättningens förfallodatum `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`:

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `displayName` | (Valfritt) Ett nytt läsbart namn för datauppsättningens förfallokonfiguration. |
| `description` | (Valfritt) En ny beskrivning av datauppsättningens förfallokonfiguration. |
| `expiry` | (Valfritt) Ett nytt förfallodatum eller datum och tid i ISO 8601-format. Om bara ett datum anges blir standardvärdet midnatt UTC. Utgångsdatumet måste vara **minst 24 timmar**. |

>[!NOTE]
>
>Minst ett av dessa fält måste anges i begäran.

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och den uppdaterade konfigurationen för förfallodatum för datauppsättning.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `ttlId` | Den unika identifieraren för den uppdaterade datauppsättningens förfallokonfiguration. |
| `datasetId` | Den unika identifieraren för datauppsättningen. |
| `datasetName` | Datauppsättningens namn. |
| `sandboxName` | Sandlådan där den här datauppsättningens förfallodatum är konfigurerad. |
| `displayName` | Visningsnamnet för datauppsättningens förfallokonfiguration. |
| `description` | En beskrivning av datauppsättningens förfallokonfiguration. |
| `imsOrg` | Organisations-ID som är associerat med den här konfigurationen. |
| `status` | Den aktuella statusen för datauppsättningens förfallokonfiguration.<br>En av: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Den schemalagda förfallotidsstämpeln för datauppsättningen. |
| `updatedAt` | Tidsstämpeln för den senaste uppdateringen. |
| `updatedBy` | Identifieraren och e-postadressen för den användare eller tjänst som senast uppdaterade förfallokonfigurationen för datauppsättningen. |

{style="table-layout:auto"}

Ett misslyckat svar returnerar HTTP-statusen 404 (Hittades inte) om det inte finns någon sådan förfallotid för datauppsättningen.

## Avbryt förfallodatum för en datauppsättning {#delete}

Avbryt en väntande förfallokonfiguration för datauppsättning genom att göra en DELETE-begäran till `/ttl/{ID}`.

>[!NOTE]
>
>Det går bara att avbryta förfallodatum för datauppsättningar i statusen `pending`. Om du försöker avbryta ett förfallodatum som redan är `executing`, `completed` eller `cancelled` returneras HTTP 400 (Ogiltig begäran).

**API-format**

```http
DELETE /ttl/{ID}
```

| Parameter | Beskrivning |
| --- | --- |
| `{ID}` | Den unika identifieraren för datauppsättningens förfallokonfiguration. Du kan antingen ange ett förfallodatum-ID för datauppsättningen eller ett datauppsättnings-ID. |

{style="table-layout:auto"}

**Begäran**

Följande begäran avbryter en förfallotid för en datauppsättning med ID `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 (OK) och den avbrutna konfigurationen för förfallodatum. Inte för att förfallodatumets `status`-attribut är inställt på `cancelled`.

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Egenskap | Beskrivning |
|---|---|
| `ttlId` | Den unika identifieraren för den borttagna datauppsättningens förfallokonfiguration. |
| `datasetId` | Den unika identifieraren för datauppsättningen. |
| `datasetName` | Datauppsättningens namn. |
| `sandboxName` | Sandlådan där den här datauppsättningens förfallotid är konfigurerad. |
| `displayName` | Visningsnamnet för datauppsättningens förfallokonfiguration. |
| `description` | En beskrivning av datauppsättningens förfallokonfiguration. |
| `imsOrg` | Din unika organisationsidentifierare som är associerad med den här konfigurationen. |
| `status` | Den aktuella statusen för datauppsättningens förfallokonfiguration.<br>En av: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | Den schemalagda förfallotidsstämpeln för datauppsättningen. |
| `updatedAt` | Tidsstämpeln för den senaste uppdateringen. |
| `updatedBy` | Identifieraren och e-postadressen för den användare eller tjänst som senast uppdaterade förfallokonfigurationen för datauppsättningen. |

**Exempel 400 (felaktig begäran) svar**

Ett 400-fel inträffar när du försöker avbryta en datauppsättning som har en `executing`-, `completed`- eller `cancelled`-förfallokonfiguration.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Ett 404-fel inträffar när ett försök görs att avbryta en förfallotid för en datauppsättning som redan är `completed` eller `cancelled`.

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

