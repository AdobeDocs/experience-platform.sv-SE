---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-slutpunkt för mått
topic: developer guide
description: Lär dig hur du hämtar mätvärden för observerbarhet i Experience Platform med API:t för observabilitetsinsikter.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 1%

---


# Måttslutpunkt

Mätvärden för observerbarhet ger insikt i användningsstatistik, historiska trender och resultatindikatorer för olika funktioner i Adobe Experience Platform. Med `/metrics`-slutpunkten i [!DNL Observability Insights API] kan du hämta mätdata för din organisations aktivitet i [!DNL Platform] programmatiskt.

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få länkar till relaterad dokumentation, en guide till hur du läser exempelanropen för API i det här dokumentet och viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform]-API.

## Hämta mätvärden för observerbarhet

Det finns två metoder som stöds för att hämta metadata med API:

* [Version 1](#v1): Ange mätvärden med hjälp av frågeparametrar.
* [Version 2](#v2): Ange och tillämpa filter på mått med JSON-nyttolast.

### Version 1 {#v1}

Du kan hämta mätdata genom att göra en GET-begäran till `/metrics`-slutpunkten och ange mätvärden med hjälp av frågeparametrar.

**API-format**

Minst ett mått måste anges i parametern `metric`. Andra frågeparametrar är valfria för filtrering av resultat.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beskrivning |
| --- | --- |
| `{METRIC}` | Det mätvärde som du vill visa. När du kombinerar flera mätvärden i ett enda anrop måste du använda ett et-tecken (`&`) för att separera enskilda mätvärden. Exempel, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | Identifieraren för en viss [!DNL Platform]-resurs vars mätvärden du vill visa. Detta ID kan vara valfritt, obligatoriskt eller inte tillämpligt beroende på vilka mätvärden som används. I [bilagan](#available-metrics) finns en lista med tillgängliga mått, inklusive vilka ID som stöds (både obligatoriska och valfria) för varje mätvärde. |
| `{DATE_RANGE}` | Datumintervallet för de mätvärden som du vill visa, i ISO 8601-format (till exempel `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Begäran**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Svar**

Ett lyckat svar returnerar en lista med objekt, där var och en innehåller en tidsstämpel inom det angivna `dateRange` och motsvarande värden för de mått som anges i sökvägen till begäran. Om `id` för en [!DNL Platform]-resurs ingår i sökvägen för begäran, gäller resultaten bara för den aktuella resursen. Om `id` utelämnas gäller resultatet för alla tillämpliga resurser i IMS-organisationen.

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### Version 2 {#v2}

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "aggregator": "sum",
            "downsample": "sum"
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
| `granularity` | Ett valfritt fält som anger ett tidsintervall för att dividera mätdata med. Värdet `DAY` returnerar till exempel mått för varje dag mellan `start`- och `end`-datumet, medan värdet `MONTH` grupperar mätresultaten per månad i stället. När du använder det här fältet måste även en motsvarande `downsample`-egenskap anges för att ange den aggregeringsfunktion som data ska grupperas med. |
| `metrics` | En array med objekt, en för varje mätvärde som du vill hämta. |
| `name` | Namnet på ett mätvärde som identifieras av observabilitetsinsikter. Se [bilagan](#available-metrics) för en fullständig lista över godkända måttnamn. |
| `filters` | Ett valfritt fält där du kan filtrera mätvärden efter specifika datauppsättningar. Fältet är en array med objekt (ett för varje filter), där varje objekt innehåller följande egenskaper: <ul><li>`name`: Den typ av entitet som mätvärden ska filtreras mot. För närvarande stöds bara `dataSets`.</li><li>`value`: ID för en eller flera datauppsättningar. Flera datauppsättnings-ID:n kan anges som en enda sträng, där varje ID avgränsas med lodräta streck (`|`).</li><li>`groupBy`: Om värdet är true visar det att motsvarande  `value` representerar flera datauppsättningar vars mätresultat ska returneras separat. Om värdet är false grupperas mätresultaten för de datauppsättningarna tillsammans.</li></ul> |
| `aggregator` | Anger den aggregeringsfunktion som ska användas för att gruppera poster med flera serier till enstaka resultat. Mer information om tillgängliga aggregerare finns i [OpenTSDB-dokumentationen](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html). |
| `downsample` | Ett valfritt fält som gör att du kan ange en aggregeringsfunktion för att minska samplingsfrekvensen för mätdata genom att sortera fält i intervall (eller&quot;bucket&quot;). Intervallet för nedsamplingen bestäms av egenskapen `granularity`. Mer information om nedsampling finns i [OpenTSDB-dokumentationen](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html). |

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
| `groupBy` | Om flera datauppsättningar har angetts i egenskapen `filter` för ett mätresultat, och alternativet `groupBy` har angetts till true i begäran, kommer det här objektet att innehålla ID:t för datauppsättningen som motsvarande `dps`-egenskap gäller för.<br><br>Om det här objektet verkar vara tomt i svaret gäller motsvarande  `dps` egenskap för alla datamängder som finns i  `filters` arrayen (eller alla datamängder i  [!DNL Platform] om inga filter har angetts). |
| `dps` | Returnerade data för angivet mått, filter och tidsintervall. Varje nyckel i det här objektet representerar en tidsstämpel med ett motsvarande värde för det angivna måttet. Tidsperioden mellan varje datapunkt beror på `granularity`-värdet som anges i begäran. |

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med slutpunkten `/metrics`.

### Tillgängliga mått {#available-metrics}

I följande tabeller visas alla mätvärden som visas av [!DNL Observability Insights], uppdelade efter tjänsten [!DNL Platform]. Varje mätvärde innehåller en beskrivning och en godkänd ID-frågeparameter.

>[!NOTE]
>
>Alla ID-frågeparametrar i listan är valfria om inget annat anges.

#### [!DNL Data Ingestion] {#ingestion}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Data Ingestion]. Mätvärden i **fet** är mätvärden för direktuppspelad konsumtion.

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Totalt antal datauppsättningar som skapats. | Ej tillämpligt |
| timeseries.ingestion.dataset.size | Kumulativ storlek för alla data som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.dailysize | Storlek på data som hämtas dagligen för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.batchfailed.count | Antal misslyckade batchar för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.batchsuccess.count | Antal batchar som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.ingestion.dataset.recordsuccess.count | Antal poster som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.total.messages.rate** | Totalt antal meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.valid.messages.rate** | Totalt antal giltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | Totalt antal ogiltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.type.count** | Totalt antal ogiltiga typmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.range.count** | Totalt antal ogiltiga intervallmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.format.count** | Totalt antal ogiltiga formatmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.pattern.count** | Totalt antal ogiltiga mönstermeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.presence.count** | Totalt antal ogiltiga närvaromeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.enum.count** | Totalt antal ogiltiga enum-meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.unclassified.count** | Totalt antal ogiltiga oklassificerade meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.validation.category.unknown.count** | Totalt antal ogiltiga &quot;okända&quot; meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| **timeseries.data.collection.inlet.total.messages.receive** | Totalt antal meddelanden som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Total storlek på data som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.success** | Totalt antal lyckade HTTP-anrop till ett dataintag eller till alla datainmatningar. | Intag-ID |
| **timeseries.data.collection.inlet.error** | Totalt antal misslyckade HTTP-anrop till en datainmatning eller till alla datainmatningar. | Intag-ID |

#### [!DNL Identity Service] {#identity}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Identity Service].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Antal poster som skrivits till datakällan av [!DNL Identity Service], för en datauppsättning eller alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.identity.dataset.recordfailed.count | Antal poster som misslyckades med [!DNL Identity Service], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Antal identitetsposter som har importerats för ett namnområde. | Namnområdes-ID (**Obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Antal Identity-poster som misslyckades av ett namnutrymme. | Namnområdes-ID (**Obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Antal Identitetsposter som hoppats över av ett namnutrymme. | Namnområdes-ID (**Obligatoriskt**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för ett namnutrymme. | Namnområdes-ID (**Obligatoriskt**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Antal unika diagramsymboler som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för IMS-organisationen för en viss grafikstyrka (&quot;unknown&quot;,&quot;svag&quot; eller&quot;strong&quot;). | Diagramstyrka (**Obligatorisk**) |

#### [!DNL Privacy Service] {#privacy}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Privacy Service].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Totalt antal jobb skapade från GDPR. | ENV (**Krävs**) |
| timeseries.gdpr.jobs.completedjobs.count | Totalt antal slutförda jobb från GDPR. | ENV (**Krävs**) |
| timeseries.gdpr.jobs.errorjobs.count | Totalt antal feljobb från GDPR. | ENV (**Krävs**) |

#### [!DNL Query Service] {#query}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Query Service].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Totalt antal icke återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.scheduledrecurring.count | Totalt antal återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchquery.count | Totalt antal utförda gruppfrågor. | Ej tillämpligt |
| timeseries.queryservice.query.scheduledquery.count | Totalt antal utförda schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.interactivequery.count | Totalt antal utförda interaktiva frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchfrompsqlquery.count | Totalt antal utförda batchfrågor från PSQL. | Ej tillämpligt |

#### [!DNL Real-time Customer Profile] {#profile}

I följande tabell visas måtten för [!DNL Real-time Customer Profile].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Antal poster som har lästs från [!DNL Data Lake] av [!DNL Profile], för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.profiles.dataset.recordsuccess.count | Antal poster som skrivits till datakällan av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.recordfailed.count | Antal poster som misslyckades med [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.batchsuccess.count | Antal [!DNL Profile] batchar som har kapslats för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.batchfailed.count | Antal [!DNL Profile] batchar som misslyckades för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| platform.ups.ingest.streaming.request.m1_rate | Frekvens för inkommande begäran. | IMS-organisation (**Krävs**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Andelen lyckade intag. | IMS-organisation (**Krävs**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Frekvens för nya poster som har importerats för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för skapandebegäran för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tidsstämpel för senaste begäran om att skapa post för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för uppdateringsbegäran för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tidsstämpel för senaste begäran om uppdatering av post för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Genomsnittlig poststorlek. | IMS-organisation (**Krävs**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Frekvens för uppdateringsbegäranden för poster som har importerats för en datauppsättning. | Datauppsättnings-ID (**Obligatoriskt**) |

### Felmeddelanden

Svar från `/metrics`-slutpunkten kan returnera felmeddelanden under vissa förhållanden. Dessa felmeddelanden returneras i följande format:

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
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
| `report` | Innehåller sammanhangsbaserad information om felet, inklusive den sandlåda och den IMS-organisation som används i åtgärden som utlöste felet. |

I följande tabell visas de olika felkoderna som kan returneras av API:t:

| Felkod | Titel | Beskrivning |
| --- | --- | --- |
| `INSGHT-1000-400` | Ogiltig nyttolast för begäran | Något var fel med nyttolasten för begäran. Kontrollera att du matchar nyttolastens formatering exakt som visas [ovan](#v2). Alla möjliga orsaker kan utlösa det här felet:<ul><li>Obligatoriska fält som `aggregator` saknas</li><li>Ogiltiga mått</li><li>Begäran innehåller en ogiltig aggregator</li><li>Ett startdatum infaller efter ett slutdatum</li></ul> |
| `INSGHT-1001-400` | Mätningsfrågan misslyckades | Det uppstod ett fel när mätdatabasen skulle frågas på grund av en felaktig begäran eller att själva frågan inte kunde tolkas. Kontrollera att din begäran är korrekt formaterad innan du försöker igen. |
| `INSGHT-1001-500` | Mätningsfrågan misslyckades | Det uppstod ett fel när mätdatabasen skulle frågas på grund av ett serverfel. Försök igen. Om problemet kvarstår kan du kontakta Adobe support. |
| `INSGHT-1002-500` | Tjänstfel | Begäran kunde inte behandlas på grund av ett internt fel. Försök igen. Om problemet kvarstår kan du kontakta Adobe support. |
| `INSGHT-1003-401` | Valideringsfel för sandlådan | Begäran kunde inte behandlas på grund av ett valideringsfel i sandlådan. Kontrollera att namnet på sandlådan som du angav i rubriken `x-sandbox-name` representerar en giltig, aktiverad sandlåda för din IMS-organisation innan du försöker utföra begäran igen. |
