---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-slutpunkt för mått
description: Lär dig hur du hämtar mätvärden för observerbarhet i Experience Platform med API:t för observationsinsikter.
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 39eda018611d0244eaff908e924afa93dc46e14d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 1%

---

# Måttslutpunkt

Mätvärden för observerbarhet ger insikt i användningsstatistik, historiska trender och resultatindikatorer för olika funktioner i Adobe Experience Platform. Med slutpunkten `/metrics` i [!DNL Observability Insights API] kan du hämta mätdata för organisationens aktivitet i [!DNL Platform] programmatiskt.

>[!NOTE]
>
>Den tidigare versionen av måttslutpunkten (V1) har tagits bort. Det här dokumentet fokuserar enbart på den aktuella versionen (V2). Mer information om V1-slutpunkten för äldre implementeringar finns i [API-referensen](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa ett [!DNL Experience Platform] -API.

## Hämta mätvärden för observerbarhet

Du kan hämta mätdata genom att göra en begäran om POST till `/metrics`-slutpunkten och ange de mätvärden som du vill hämta i nyttolasten.

**API-format**

```http
POST /metrics
```

**Begäran**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| Egenskap | Beskrivning |
| --- | --- |
| `start` | Det tidigaste datum/den tidigaste tid från vilken mätdata ska hämtas. |
| `end` | Det senaste datumet/den senaste tiden från vilket mätdata ska hämtas. |
| `granularity` | Ett valfritt fält som anger tidsintervallet för att dividera mätdata med. Värdet `DAY` returnerar till exempel mått för varje dag mellan `start` och `end`, medan värdet `MONTH` grupperar mätresultaten per månad i stället. |
| `metrics` | En array med objekt, en för varje mätvärde som du vill hämta. |
| `name` | Namnet på ett mätvärde som identifieras av observabilitetsinsikter. I [bilagan](#available-metrics) finns en fullständig lista över giltiga måttnamn. |
| `filters` | Ett valfritt fält där du kan filtrera mätvärden efter specifika datauppsättningar. Fältet är en array med objekt (ett för varje filter), där varje objekt innehåller följande egenskaper: <ul><li>`name`: Den typ av entitet som mätvärden ska filtreras mot. För närvarande stöds bara `dataSets`.</li><li>`value`: ID för en eller flera datauppsättningar. Flera datauppsättnings-ID kan anges som en enda sträng, där varje ID avgränsas med lodräta streck (`\|`).</li><li>`groupBy`: Om värdet är true anger det att motsvarande `value` representerar flera datauppsättningar vars mätresultat ska returneras separat. Om värdet är false grupperas mätresultaten för de datauppsättningarna tillsammans.</li></ul> |
| `aggregator` | Anger den aggregeringsfunktion som ska användas för att gruppera poster med flera serier till enstaka resultat. De aggregerare som stöds för närvarande är min, max, sum och avg beroende på metrisk definition. |

{style="table-layout:auto"}

**Svar**

Ett lyckat svar returnerar de resulterande datapunkterna för de mätvärden och filter som anges i begäran.

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `metricResponses` | En array vars objekt representerar alla mått som anges i begäran. Varje objekt innehåller information om filterkonfigurationen och returnerade mätdata. |
| `metric` | Namnet på ett av måtten som anges i begäran. |
| `filters` | Filterkonfigurationen för det angivna måttet. |
| `datapoints` | En array vars objekt representerar resultatet av det angivna måttet och filtren. Antalet objekt i arrayen beror på de filteralternativ som anges i begäran. Om inga filter har angetts innehåller arrayen bara ett objekt som representerar alla datauppsättningar. |
| `groupBy` | Om flera datauppsättningar har angetts i egenskapen `filter` för ett mätresultat och alternativet `groupBy` har angetts till true i begäran, kommer objektet att innehålla ID:t för datauppsättningen som motsvarande `dps` -egenskap gäller för.<br><br>Om det här objektet verkar vara tomt i svaret gäller motsvarande `dps` -egenskap för alla datamängder som finns i `filters` -arrayen (eller alla datamängder i [!DNL Platform] om inga filter har angetts). |
| `dps` | Returnerade data för angivet mått, filter och tidsintervall. Varje nyckel i det här objektet representerar en tidsstämpel med ett motsvarande värde för det angivna måttet. Tidsperioden mellan varje datapunkt beror på det `granularity`-värde som anges i begäran. |

{style="table-layout:auto"}

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med slutpunkten `/metrics`.

### Tillgängliga mått {#available-metrics}

I följande tabeller visas alla mätvärden som visas av [!DNL Observability Insights], uppdelade efter [!DNL Platform]-tjänst. Varje mätvärde innehåller en beskrivning och en godkänd ID-frågeparameter.

>[!NOTE]
>
>Alla ID-frågeparametrar i listan är valfria om inget annat anges.

#### [!DNL Data Ingestion] {#ingestion}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Data Ingestion]. Mätvärden i **fet** är mätvärden för direktuppspelad konsumtion.

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | Kumulativ storlek för alla data som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.dailysize | Storlek på data som hämtas dagligen för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.batchfailed.count | Antal misslyckade batchar för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.batchsuccess.count | Antal batchar som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.recordsuccess.count | Antal poster som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.presence.count** | Totalt antal ogiltiga närvaromeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.inlet.total.messages.receive** | Totalt antal meddelanden som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Total storlek på data som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.success** | Totalt antal lyckade HTTP-anrop till ett dataintag eller till alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.error** | Totalt antal misslyckade HTTP-anrop till en datainmatning eller till alla datainmatningar. | Intag-ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Identity Service].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Antal poster som skrivits till deras datakälla av [!DNL Identity Service], för en datamängd eller alla datamängder. | Datauppsättnings-ID |
| timeseries.identity.dataset.recordfailed.count | Antal poster som misslyckades av [!DNL Identity Service], för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Antal Identitetsposter som hoppats över. | Organisations-ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för din organisation. | N/A |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för ett namnutrymme. | Namnområdes-ID (**Obligatoriskt**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för din organisation för en viss grafikstyrka (&quot;unknown&quot;,&quot;svag&quot; eller&quot;strong&quot;). | Diagramstyrka (**krävs**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

Följande tabell visar mätvärden för [!DNL Real-Time Customer Profile].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Antal poster som har lästs från [!DNL Data Lake] av [!DNL Profile], för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.profiles.dataset.recordsuccess.count | Antal poster som skrivits till deras datakälla av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.batchsuccess.count | Antal [!DNL Profile] batchar som har kapslats in för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |

{style="table-layout:auto"}

### Felmeddelanden

Svar från slutpunkten `/metrics` kan returnera felmeddelanden under vissa förhållanden. Dessa felmeddelanden returneras i följande format:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `title` | En sträng som innehåller felmeddelandet och den möjliga orsaken till felet. |
| `report` | Innehåller sammanhangsbaserad information om felet, inklusive den sandlåda och organisation som används i åtgärden som utlöste felet. |

{style="table-layout:auto"}

I följande tabell visas de olika felkoderna som kan returneras av API:t:

| Felkod | Titel | Beskrivning |
| --- | --- | --- |
| `INSGHT-1000-400` | Ogiltig nyttolast för begäran | Det uppstod ett fel med nyttolasten för begäran. Kontrollera att du matchar nyttolastens formatering exakt så som visas [ovan](#v2). Alla möjliga orsaker kan utlösa det här felet:<ul><li>Obligatoriska fält som `aggregator` saknas</li><li>Ogiltiga mått</li><li>Begäran innehåller en ogiltig aggregator</li><li>Ett startdatum infaller efter ett slutdatum</li></ul> |
| `INSGHT-1001-400` | Mätningsfrågan misslyckades | Det uppstod ett fel när mätdatabasen skulle frågas på grund av en felaktig begäran eller att själva frågan inte kunde tolkas. Kontrollera att din begäran är korrekt formaterad innan du försöker igen. |
| `INSGHT-1001-500` | Mätningsfrågan misslyckades | Det uppstod ett fel när mätdatabasen skulle frågas på grund av ett serverfel. Försök igen. Om problemet kvarstår kan du kontakta Adobe support. |
| `INSGHT-1002-500` | Tjänstfel | Begäran kunde inte behandlas på grund av ett internt fel. Försök igen. Om problemet kvarstår kan du kontakta Adobe support. |
| `INSGHT-1003-401` | Valideringsfel för sandlådan | Begäran kunde inte behandlas på grund av ett valideringsfel i sandlådan. Kontrollera att namnet på sandlådan som du angav i rubriken `x-sandbox-name` representerar en giltig, aktiverad sandlåda för din organisation innan du försöker utföra begäran igen. |

{style="table-layout:auto"}
