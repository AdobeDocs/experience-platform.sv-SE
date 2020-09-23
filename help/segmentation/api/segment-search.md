---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;segment;Segment;search;segment search;
title: Slutpunkt för segmentsökning
topic: guide
description: Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid. Den här handboken innehåller information som hjälper dig att förstå segmentsökning bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Slutpunkt för segmentsökning

Segmentsökning används för att söka efter fält som finns i olika datakällor och returnera dem i nära realtid.

Den här handboken innehåller information som hjälper dig att förstå segmentsökning bättre och innehåller exempel på API-anrop för att utföra grundläggande åtgärder med API:t.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service] API:t. Innan du fortsätter bör du läsa [Komma igång-guiden](./getting-started.md) för att få viktig information som du behöver veta för att kunna anropa API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

Förutom de obligatoriska rubrikerna som beskrivs i avsnittet Komma igång, kräver alla begäranden till slutpunkten för segmentsökning följande ytterligare rubrik:

- x-ups-search-version: &quot;1.0&quot;

### Sök i flera namnutrymmen

Den här sökslutpunkten kan användas för att söka i olika namnutrymmen och returnera en lista med sökresultat. Flera parametrar kan användas, avgränsade med et-tecken (&amp;).

**API-format**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parametrar | Beskrivning |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoriskt)** Där {SCHEMA} representerar schemaklassvärdet som är associerat med sökobjekten. För närvarande `_xdm.context.segmentdefinition` stöds bara. |
| `s={SEARCH_TERM}` | *(Valfritt)* Där {SEARCH_TERM} representerar en fråga som följer Microsofts implementering av [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om ingen sökterm har angetts `schema.name` returneras alla poster som är kopplade till den. En mer detaljerad förklaring finns i [bilagan](#appendix) till det här dokumentet. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med följande information.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Sök efter enskilda entiteter

Sökslutpunkten kan användas för att hämta en lista över alla fulltextindexerade objekt inom det angivna namnutrymmet. Flera parametrar kan användas, avgränsade med et-tecken (&amp;).

**API-format**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parametrar | Beskrivning |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoriskt)** Där {SCHEMA} innehåller det schemaklassvärde som är associerat med sökobjekten. För närvarande `_xdm.context.segmentdefinition` stöds bara. |
| `namespace={NAMESPACE}` | **(Obligatoriskt)** Där {NAMESPACE} innehåller det namnutrymme som du vill söka i. |
| `s={SEARCH_TERM}` | *(Valfritt)* Där {SEARCH_TERM} innehåller en fråga som överensstämmer med Microsofts implementering av [Lucenes söksyntax](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Om ingen sökterm har angetts `schema.name` returneras alla poster som är kopplade till den. En mer detaljerad förklaring finns i [bilagan](#appendix) till det här dokumentet. |
| `entityId={ENTITY_ID}` | *(Valfritt)* Begränsar sökningen till i den angivna mappen, som anges med {ENTITY_ID}. |
| `limit={LIMIT}` | *(Valfritt)* Där {LIMIT} representerar antalet sökresultat som ska returneras. Standardvärdet är 50. |
| `page={PAGE}` | *(Valfritt)* Där {PAGE} representerar sidnumret som används för att sidnumrera resultaten av den fråga som söks igenom. Observera att sidnumret börjar på **0**. |


**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med resultat som matchar sökfrågan.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Hämta strukturinformation om ett sökobjekt

Den här sökslutpunkten kan användas för att hämta strukturinformation om det begärda sökobjektet.

**API-format**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parametrar | Beskrivning |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Obligatoriskt)** Där {SCHEMA} innehåller det schemaklassvärde som är associerat med sökobjekten. För närvarande `_xdm.context.segmentdefinition` stöds bara. |
| `namespace={NAMESPACE}` | **(Obligatoriskt)** Där {NAMESPACE} innehåller det namnutrymme som du vill söka i. |
| `entityId={ENTITY_ID}` | **(Obligatoriskt)** ID:t för det sökobjekt som du vill hämta strukturinformationen om, som anges med {ENTITY_ID}. |

**Begäran**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med detaljerad strukturinformation om det begärda sökobjektet.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Nästa steg

När du har läst den här guiden får du nu en bättre förståelse för hur segmentsökning fungerar.

## Bilaga {#appendix}

I följande avsnitt finns mer information om hur söktermer fungerar. Sökfrågor skrivs på följande sätt: `s={FieldName}:{SearchExpression}`. Om du till exempel vill söka efter ett segment med namnet AAM eller [!DNL Platform]använder du följande sökfråga: `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] För bästa praxis bör sökuttrycket vara HTML-kodat, som i exemplet ovan.

### Sökfält {#search-fields}

I följande tabell visas de fält som kan genomsökas i sökfrågeparametern.

| Fältnamn | Beskrivning |
| ---------- | ----------- |
| folderId | Mappen eller mapparna som har mapp-ID:t för den angivna sökningen. |
| folderLocation | Platsen eller platserna som har mapplatsen för den angivna sökningen. |
| parentFolderId | Segmentet eller mappen som har det överordnade mapp-ID som du har angett för sökningen. |
| segmentId | Segmentet matchar segment-ID:t för den angivna sökningen. |
| segmentName | Segmentet matchar segmentnamnet i den angivna sökningen. |
| segmentDescription | Segmentet matchar segmentbeskrivningen i den angivna sökningen. |

### Sökuttryck {#search-expression}

I följande tabell visas hur sökfrågor fungerar när du använder API:t för segmentsökning.

>!![NOTE] Följande exempel visas i ett format som inte är HTML-kodat för bättre tydlighet. För bästa praxis kodar HTML ditt sökuttryck.

| Exempel på sökuttryck | Beskrivning |
| ------------------------- | ----------- |
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
