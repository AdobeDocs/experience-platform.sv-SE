---
solution: Experience Platform
title: Förhandsgranskningar och uppskattningar av API-slutpunkter
description: I takt med att segmentdefinitionen utvecklas kan du använda verktygen för uppskattning och förhandsgranskning i Adobe Experience Platform för att se information på sammanfattningsnivå för att säkerställa att du isolerar den förväntade målgruppen.
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Förhandsgranska och beräkna slutpunkter

När du utvecklar en segmentdefinition kan du använda verktygen för uppskattning och förhandsgranskning i Adobe Experience Platform för att se information på sammanfattningsnivå för att se till att du isolerar den målgrupp du förväntar dig.

* **Förhandsvisningar** innehåller sidnumrerade listor med kvalificeringsprofiler för en segmentdefinition, så att du kan jämföra resultaten med vad du förväntar dig.

* **Uppskattningar** innehåller statistisk information om en segmentdefinition, t.ex. förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse.

>[!NOTE]
>
>Om du vill få tillgång till liknande mått som rör kundprofildata i realtid, t.ex. totalt antal profilfragment och sammanfogade profiler inom specifika namnutrymmen eller hela profildatalagret, ska du läsa [profilförhandsgranskningsguiden (förhandsvisningsexempelstatus)](../../profile/api/preview-sample-status.md) som ingår i utvecklarhandboken för profil-API.

## Komma igång

Slutpunkterna som används i den här guiden ingår i [!DNL Adobe Experience Platform Segmentation Service]-API:t. Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## Hur uppskattningar genereras

När inmatningen av poster i profilarkivet ökar eller minskar det totala antalet profiler med mer än 5 %, utlöses ett samplingsjobb för att uppdatera antalet. Hur datainsamling utlöses beror på intagsmetoden:

* **Gruppinmatning:** Om tröskelvärdet på 5 % ökning eller minskning är uppfyllt, körs ett jobb för att uppdatera antalet inom 15 minuter efter att en batch har importerats till profilbutiken.
* **Direktuppspelningsinmatning:** För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller inte. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet.

Exempelstorleken för sökningen beror på det totala antalet enheter i din profilbutik. De här exempelstorlekarna visas i följande tabell:

| Enheter i profilarkivet | Samplingsstorlek |
| ------------------------- | ----------- |
| Mindre än 1 miljon | Fullständig datauppsättning |
| 1 till 20 miljoner | 1 miljon |
| Över 20 miljoner | 5 % av det totala |

>[!NOTE]
>
>Uppskattningar tar i allmänhet 10 till 15 sekunder att köra, med början med en grov uppskattning och förfining allt eftersom fler poster läses.

## Skapa en ny förhandsgranskning {#create-preview}

Du kan skapa en ny förhandsgranskning genom att göra en POST-förfrågan till slutpunkten `/preview`.

>[!NOTE]
>
>Ett uppskattningsjobb skapas automatiskt när ett förhandsgranskningsjobb skapas. Dessa två jobb delar samma ID.

**API-format**

```http
POST /preview
```

**Begäran**

+++ Ett exempel på en förfrågan om att skapa en förhandsgranskning.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `predicateExpression` | PQL-uttrycket som data ska frågas efter. |
| `predicateType` | Predikattypen för frågeuttrycket under `predicateExpression`. För närvarande är det enda tillåtna värdet för den här egenskapen `pql/text`. |
| `predicateModel` | Namnet på schemaklassen [!DNL Experience Data Model] (XDM) som profildata baseras på. |
| `graphType` | Den diagramtyp som du vill hämta klustret från. Värdena som stöds är `none` (utför ingen identitetssammanfogning) och `pdg` (utför identitetssammanfogning baserat på ditt privata identitetsdiagram). |

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 201 (Skapad) med information om den nya förhandsgranskningen.

+++ Ett exempelsvar när du skapar en förhandsvisning.

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `state` | Det aktuella läget för förhandsgranskningsjobbet. När den skapas är den i läget&quot;NYTT&quot;. Därefter kommer det att vara i tillståndet &quot;RUNNING&quot; tills bearbetningen är klar, och då blir det &quot;RESULT_READY&quot; eller &quot;FAILED&quot;. |
| `previewId` | ID:t för förhandsgranskningsjobbet, som ska användas i sökningssyfte vid visning av en uppskattning eller förhandsvisning, enligt beskrivningen i nästa avsnitt. |

+++

## Hämta resultatet från en viss förhandsgranskning {#get-preview}

Du kan hämta detaljerad information om en viss förhandsgranskning genom att göra en GET-förfrågan till `/preview`-slutpunkten och ange förhandsgransknings-ID:t i begärandesökvägen.

**API-format**

```http
GET /preview/{PREVIEW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{PREVIEW_ID}` | Värdet `previewId` för den förhandsgranskning som du vill hämta. |

**Begäran**

+++ Ett exempel på en begäran om att hämta en förhandsgranskning.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

+++ Ett exempelsvar när du hämtar en förhandsgranskning.

Ett lyckat svar returnerar HTTP-status 200 med detaljerad information om den angivna förhandsgranskningen.

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `results` | En lista över enhets-ID:n, tillsammans med deras relaterade identiteter. De angivna länkarna kan användas för att leta upp de angivna entiteterna med hjälp av API-slutpunkten [för profilåtkomst](../../profile/api/entities.md). |

+++

## Hämta resultaten från ett specifikt uppskattningsjobb {#get-estimate}

När du har skapat ett förhandsgranskningsjobb kan du använda dess `previewId` i sökvägen för en GET-begäran till `/estimate`-slutpunkten för att visa statistisk information om segmentdefinitionen, inklusive förväntad målgruppsstorlek, konfidensintervall och felstandardavvikelse.

**API-format**

```http
GET /estimate/{PREVIEW_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{PREVIEW_ID}` | Ett uppskattningsjobb aktiveras bara när ett förhandsgranskningsjobb skapas och de två jobben har samma ID-värde för sökningssyften. Detta är det `previewId`-värde som returnerades när förhandsgranskningsjobbet skapades. |

**Begäran**

Följande begäran hämtar resultatet av ett specifikt uppskattningsjobb.

+++ En exempelbegäran om att hämta ett uppskattningsjobb.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Svar**

Ett lyckat svar returnerar HTTP-status 200 med information om uppskattningsjobbet.

+++ Ett samplingssvar när ett uppskattningsjobb hämtas.

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | En array med objekt som visar antalet profiler i segmentdefinitionen uppdelade efter identitetsnamnutrymme. Det totala antalet profiler per namnutrymme (genom att lägga ihop värdena som visas för varje namnutrymme) kan vara högre än antalet profiler eftersom en profil kan kopplas till flera namnutrymmen. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden. |
| `state` | Det aktuella läget för förhandsgranskningsjobbet. Läget kommer att vara &quot;RUNNING&quot; tills bearbetningen är slutförd, och då blir det &quot;RESULT_READY&quot; eller &quot;FAILED&quot;. |
| `_links.preview` | När `state` är &quot;RESULT_READY&quot; tillhandahåller det här fältet en URL för att visa uppskattningen. |

+++

## Nästa steg

När du har läst den här guiden bör du få en bättre förståelse för hur du arbetar med förhandsgranskningar och uppskattningar med segmenterings-API:t. Om du vill lära dig hur du får åtkomst till mått som hör till kundprofildata i realtid, t.ex. totalt antal profilfragment och sammanfogade profiler inom specifika namnutrymmen eller hela profildatalagret, går du till [profilförhandsgranskningsguiden (`/previewsamplestatus`) ](../../profile/api/preview-sample-status.md).
