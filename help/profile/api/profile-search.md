---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# Profilsökning

Profilsökning används för att söka efter och indexera konfigurerbara fält som finns i olika datakällor och returnera dem i nära realtid.

Den här handboken innehåller information som hjälper dig att förstå profilsökningen bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

API-slutpunkterna som används i den här guiden ingår i kundprofils-API:t i realtid. Innan du fortsätter bör du läsa Utvecklarhandbok för kundprofiler i [realtid](getting-started.md).

Avsnittet [](getting-started.md) Komma igång i guiden för profilutvecklare innehåller länkar till relaterade ämnen, en guide till hur du läser exempelanrop till API:er i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa API:er för Experience Platform.

### Hämta sökresultat

Sökslutpunkten kan användas för att hämta sökresultat baserat på värdena för den obligatoriska `schema.name` parametern och ytterligare valfria frågeparametrar. Flera parametrar kan användas, avgränsade med et-tecken (&amp;).

**API-format**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parameter | Beskrivning |
|---|---|
| `schema.name` | **Obligatoriskt.** Namnet på schemaklassen som innehåller innehållet som ska sökas, skrivet i punktnotationsformat. För närvarande `schema.name=_xdm.context.segmentdefinition` stöds bara. |
| `limit` | Antalet sökresultat som ska returneras. Standardvärdet är 50. |
| `page` | Det sidnummer som används för att numrera resultatet av den sökta frågan. |
| `s` | En fråga som följer Microsofts implementering av [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om ingen sökterm har angetts `schema.name` returneras alla poster som är kopplade till den. En mer detaljerad förklaring finns i avsnittet [Sökparametrar](#search-parameters) i det här dokumentet. |
| `namespace` | Identifierar de faktiska data som ska sökas efter schemaklassen som anges i `schema.name` parametern. |
| `organization.type` | Anger innehållet i svaret. Formatet på det returnerade innehållet beror på vilka värden som används i `schema.name`. Giltiga värden `_xdm.context.segmentdefinition`är `hierarchy` eller `hierarchyinfo`. |
| `organization.id` | **Obligatoriskt om`organization.type`anges.** Ger hierarkin för den angivna organisationen när den används med hierarkin `organization.type` . |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett godkänt svar returnerar en array med objekt som uppfyller sökvillkoren. I det här exemplet returneras en lista med segmentdefinitioner eftersom `schema.name` parametern var `_xdm.context.segmentdefinition`.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Skapa provisioneringsbegäranden

Du kan skapa provisioneringsbegäranden för att aktivera profilsökning för scheman genom att göra en POST-begäran till `/search/provisioning/component/init` slutpunkten.

**Begäran**

>[!CAUTION]
>Denna POST-begäran innehåller ingen nyttolast och därför krävs ingen Content-Type-rubrik. Dessutom finns det ingen sandlåderubrik eftersom alla data skickas till en global sandlåda.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) och följande meddelande:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Hantera konfigurationsbegäranden

Konfigurationsslutpunkten kan användas för att ställa in rätt index, indexerare och datakällanslutningar för en ny IMS-organisation. Två egenskaper krävs för att hantera konfigurationsbegäranden: `databaseName` och `containerName`.

`databaseName` representerar namnet på profildatabasen för organisationen som ska konfigureras.

`containerName` representerar namnet på behållaren ifylld av en dataanslutning, vilket är vad som läses under konfigurationen. Det finns två värden för `containerName`, ett eller båda kan användas i POST-begäran:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Skapa en konfigurationsbegäran

Följande API-anrop genererar den nödvändiga datakällan, indexeraren och indexet baserat på parametrarna som anges i nyttolasten för begäran.

**API-format**

```http
POST /search/configure
```

**Begäran**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Godkänd) och ett klartextmeddelande.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Ta bort en konfigurationsbegäran

Följande API-anrop tar bort matchande indexposter och tar bort indexeraren och datakällan baserat på parametrarna som anges i nyttolasten för begäran.

>[!NOTE]
>Själva indexet tas inte bort eftersom det är en delad resurs.

**API-format**

```http
DELETE /search/configure
```

**Begäran**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Svar**

Ett lyckat svar returnerar HTTP-status 202 (Godkänd) och ett klartextmeddelande.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur kundprofilsökningen i realtid fungerar. Mer information om kundprofil i realtid finns i [Kundprofilöversikt](../home.md)i realtid. Mer information om segmentering finns i [segmenteringsöversikten](../../segmentation/home.md).

## Bilaga {#appendix}

### Sökparametrar {#search-parameters}

I följande tabell visas hur sökparametern fungerar när du använder söknings-API:t.

| Sökfråga | Beskrivning |
|------------ | -----------|
| foo | Sök efter ett ord. Detta returnerar resultaten om ordet &quot;foo&quot; finns i något av de sökbara fälten. |
| foto OCH streck | En boolesk sökning. Resultatet returneras om **båda** orden &quot;foo&quot; och &quot;bar&quot; finns i något av de sökbara fälten. |
| foto ELLER fält | En boolesk sökning. Resultatet returneras om **antingen** ordet &quot;foo&quot; eller ordet &quot;bar&quot; hittas i något av de sökbara fälten. |
| foo NOT bar | En boolesk sökning. Detta returnerar resultaten om ordet &quot;foo&quot; hittas men ordet &quot;bar&quot; inte hittas i något av de sökbara fälten. |
| namn: foto OCH streck | En boolesk sökning. Resultatet returneras om **båda** orden &quot;foo&quot; och &quot;bar&quot; finns i fältet &quot;name&quot;. |
| run* | En sökning med jokertecken. Om du använder en asterisk (*) matchar 0 eller fler tecken, vilket innebär att resultatet returneras om innehållet i något av de sökbara fälten innehåller ett ord som börjar med&quot;run&quot;. Detta returnerar till exempel resultat om orden&quot;kör&quot;,&quot;kör&quot;,&quot;kör&quot; eller&quot;runner&quot; visas. |
| kamera? | En sökning med jokertecken. Använda ett frågetecken (?) matchar endast exakt ett tecken, vilket innebär att resultatet returneras om innehållet i något av de sökbara fälten börjar med &quot;cam&quot; och en extra bokstav. Detta returnerar till exempel resultat om orden &quot;läger&quot; eller &quot;kameror&quot; visas, men returnerar inga resultat om orden &quot;kamera&quot; eller &quot;campfire&quot; visas. |
| &quot;blått paraply&quot; | En frassökning. Detta returnerar resultaten om innehållet i något av de sökbara fälten innehåller den fullständiga frasen &quot;blue paraply&quot;. |
| blue\~ | En otydlig sökning. Du kan också ange redigeringsavståndet genom att placera ett tal mellan 0 och 2 efter tildetecknet (~). &quot;blue\~1&quot; skulle till exempel returnera &quot;blue&quot;, &quot;blues&quot; eller &quot;glue&quot;. Fuzzy-sökning kan **bara** användas på termer, inte på fraser. Du kan dock lägga till tildetecken i slutet av varje ord i en fras. &quot;camping\~ in\~ the\~ sommar\~&quot; skulle alltså matcha på &quot;camping in the sommar&quot;. |
| &quot;hotell flygplats&quot;\~5 | En närhetssökning. Den här typen av sökning används för att hitta termer som ligger nära varandra i ett dokument. Frasen `"hotel airport"~5` hittar till exempel termerna&quot;hotell&quot; och&quot;flygplats&quot; inom fem ord från varandra i ett dokument. |
| `/a[0-9]+b$/` | En sökning med reguljära uttryck. Vid den här typen av sökning hittas en matchning baserat på innehållet mellan snedstreck &quot;/&quot;, vilket beskrivs i klassen RegExp. Om du till exempel vill söka efter dokument som innehåller &quot;motell&quot; eller &quot;hotell&quot; anger du `/[mh]otel/`. Sökningar i reguljära uttryck matchas mot enstaka ord. |

Mer detaljerad dokumentation om frågesyntaxen finns i [Lucene-frågesyntaxens dokumentation](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
