---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tillgängliga mått
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# Måttslutpunkt

Mätvärden för observerbarhet ger insikt i användningsstatistik, historiska trender och resultatindikatorer för olika funktioner i Adobe Experience Platform. Med `/metrics` slutpunkten i [!DNL Observability Insights API] kan du hämta mätdata för organisationens aktivitet i [!DNL Platform].

## Komma igång

API-slutpunkten som används i den här guiden ingår i [[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml). Innan du fortsätter bör du läsa [Komma igång-guiden](./getting-started.md) för länkar till relaterad dokumentation, en guide till hur du läser exempelanrop till API i det här dokumentet samt viktig information om vilka huvuden som krävs för att kunna anropa valfritt [!DNL Experience Platform] -API.

## Hämta mätvärden för observerbarhet

Du kan hämta observerbarhetsvärden genom att göra en GET-förfrågan till `/metrics` slutpunkten i [!DNL Observability Insights] API:t.

**API-format**

När du använder `/metrics` slutpunkten måste minst en parameter för metrisk begäran anges. Andra frågeparametrar är valfria för filtrering av resultat.

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
| `{ID}` | Identifieraren för en viss [!DNL Platform] resurs vars mätvärden du vill visa. Detta ID kan vara valfritt, obligatoriskt eller inte tillämpligt beroende på vilka mätvärden som används. I [bilagan](#available-metrics) finns en lista över tillgängliga mätvärden samt ID:n som stöds (både obligatoriska och valfria) för varje mätvärde. |
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

Ett godkänt svar returnerar en lista med objekt, där var och en innehåller en tidsstämpel inom det angivna `dateRange` och motsvarande värden för de mått som anges i sökvägen för begäran. Om en `id` resurs är inkluderad [!DNL Platform] i den begärda sökvägen gäller resultaten endast den aktuella resursen. Om `id` utelämnas gäller resultatet alla tillämpliga resurser i IMS-organisationen.

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

## Bilaga

Följande avsnitt innehåller ytterligare information om hur du arbetar med `/metrics` slutpunkten.

### Tillgängliga mått {#available-metrics}

I följande tabeller visas alla mätvärden som exponeras av [!DNL Observability Insights], uppdelade efter [!DNL Platform] tjänst. Varje mätvärde innehåller en beskrivning och en godkänd ID-frågeparameter.

>[!NOTE]
>
>Alla ID-frågeparametrar i listan är valfria om inget annat anges.

#### [!DNL Data Ingestion] {#ingestion}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Data Ingestion]. Mätvärden i **fet stil** är mätvärden för direktuppspelad konsumtion.

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
| timeseries.identity.dataset.recordfailed.count | Antal poster som misslyckades av [!DNL Identity Service], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Antal identitetsposter som har importerats för ett namnområde. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Antal Identity-poster som misslyckades av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Antal Identitetsposter som hoppats över av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Antal unika diagramsymboler som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för IMS-organisationen för en viss grafikstyrka (&quot;unknown&quot;,&quot;svag&quot; eller&quot;strong&quot;). | Diagramstyrka (**krävs**) |

#### [!DNL Privacy Service] {#privacy}

I följande tabell visas mätvärden för Adobe Experience Platform [!DNL Privacy Service].

| Insikter - mått | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Totalt antal jobb skapade från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.jobs.completedjobs.count | Totalt antal slutförda jobb från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.jobs.errorjobs.count | Totalt antal feljobb från GDPR. | ENV (**obligatoriskt**) |

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
| timeseries.profiles.dataset.recordread.count | Antal poster som har lästs från [!DNL Data Lake] av, [!DNL Profile]för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID |
| timeseries.profiles.dataset.recordsuccess.count | Antal poster som skrivits till datakällan av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.recordfailed.count | Antal poster som misslyckades av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.batchsuccess.count | Antal [!DNL Profile] batchar som har importerats för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| timeseries.profiles.dataset.batchfailed.count | Antal misslyckade [!DNL Profile] batchar för en datamängd eller för alla datamängder. | Datauppsättnings-ID |
| platform.ups.ingest.streaming.request.m1_rate | Frekvens för inkommande begäran. | IMS-organisation (**krävs**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Andelen lyckade intag. | IMS-organisation (**krävs**) |
| platform.ups.ingest.streaming.records.created.m15_rate | Frekvens för nya poster som har importerats för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för skapandebegäran för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tidsstämpel för senaste begäran om att skapa post för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för uppdateringsbegäran för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tidsstämpel för senaste begäran om uppdatering av post för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |
| platform.ups.ingest.streaming.record.size.m1_rate | Genomsnittlig poststorlek. | IMS-organisation (**krävs**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | Frekvens för uppdateringsbegäranden för poster som har importerats för en datauppsättning. | Datauppsättnings-ID (**obligatoriskt**) |