---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tillgängliga mått
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# Lista över tillgängliga mätvärden

I följande tabeller visas alla mätvärden som exponeras av observabilitetsinsikter, uppdelade efter [!DNL Platform] tjänst. Varje mätvärde innehåller en beskrivning och en godkänd ID-frågeparameter.

## [!DNL Data Ingestion]

I följande tabell visas måtten för Adobe Experience Platform [!DNL Data Ingestion]. Mätvärden i **fet stil** är mätvärden för direktuppspelad konsumtion.

| Insikter - mått  | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Totalt antal datauppsättningar som skapats. | Ej tillämpligt |
| timeseries.ingestion.dataset.size | Kumulativ storlek för alla data som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.ingestion.dataset.dailysize | Storlek på data som hämtas dagligen för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.ingestion.dataset.batchfailed.count | Antal misslyckade batchar för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.ingestion.dataset.batchsuccess.count | Antal batchar som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.ingestion.dataset.recordsuccess.count | Antal poster som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.total.messages.rate** | Totalt antal meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.valid.messages.rate** | Totalt antal giltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.invalid.messages.rate** | Totalt antal ogiltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.type.count** | Totalt antal ogiltiga typmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.range.count** | Totalt antal ogiltiga intervallmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.format.count** | Totalt antal ogiltiga formatmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.pattern.count** | Totalt antal ogiltiga mönstermeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.presence.count** | Totalt antal ogiltiga närvaromeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.enum.count** | Totalt antal ogiltiga enum-meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.unclassified.count** | Totalt antal ogiltiga oklassificerade meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.validation.category.unknown.count** | Totalt antal ogiltiga &quot;okända&quot; meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| **timeseries.data.collection.inlet.total.messages.receive** | Totalt antal meddelanden som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID (valfritt) |
| **timeseries.data.collection.inlet.total.messages.size.receive** | Total storlek på data som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID (valfritt) |
| **timeseries.data.collection.inlet.success** | Totalt antal lyckade HTTP-anrop till ett dataintag eller till alla datainmatningar. | Intag-ID (valfritt) |
| **timeseries.data.collection.inlet.error** | Totalt antal misslyckade HTTP-anrop till en datainmatning eller till alla datainmatningar. | Intag-ID (valfritt) |

## [!DNL Identity Service]

I följande tabell visas måtten för Adobe Experience Platform [!DNL Identity Service].

| Insikter - mått  | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Antal poster som skrivits till datakällan av [!DNL Identity Service], för en datauppsättning eller alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.identity.dataset.recordfailed.count | Antal poster som misslyckades av [!DNL Identity Service], för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Antal identitetsposter som har importerats för ett namnområde. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Antal Identity-poster som misslyckades av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Antal Identitetsposter som hoppats över av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Antal unika diagramsymboler som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Antal unika identiteter som lagras i identitetsdiagrammet för IMS-organisationen för en viss grafikstyrka (&quot;unknown&quot;,&quot;svag&quot; eller&quot;strong&quot;). | Diagramstyrka (**krävs**) |

## [!DNL Privacy Service]

I följande tabell visas måtten för Adobe Experience Platform [!DNL Privacy Service].

| Insikter - mått  | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Totalt antal jobb skapade från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.jobs.completedjobs.count | Totalt antal slutförda jobb från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.jobs.errorjobs.count | Totalt antal feljobb från GDPR. | ENV (**obligatoriskt**) |

## [!DNL Query Service]

I följande tabell visas måtten för Adobe Experience Platform [!DNL Query Service].

| Insikter - mått  | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Totalt antal icke återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.scheduledrecurring.count | Totalt antal återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchquery.count | Totalt antal utförda gruppfrågor. | Ej tillämpligt |
| timeseries.queryservice.query.scheduledquery.count | Totalt antal utförda schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.interactivequery.count | Totalt antal utförda interaktiva frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchfrompsqlquery.count | Totalt antal utförda batchfrågor från PSQL. | Ej tillämpligt |

## [!DNL Real-time Customer Profile]

I följande tabell visas måtten för [!DNL Real-time Customer Profile].

| Insikter - mått  | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Antal poster som har lästs från [!DNL Data Lake] av, [!DNL Profile]för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.recordsuccess.count | Antal poster som skrivits till datakällan av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.recordfailed.count | Antal poster som misslyckades av [!DNL Profile], för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.batchsuccess.count | Antal [!DNL Profile] batchar som har importerats för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.batchfailed.count | Antal misslyckade [!DNL Profile] batchar för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| platform.ups.ingest.streaming.request.m1_rate | Frekvens för inkommande begäran. | IMS-organisation |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Andelen lyckade intag. | IMS-organisation |
| platform.ups.ingest.streaming.records.created.m15_rate | Frekvens för nya poster som har importerats för en datauppsättning. | Datauppsättnings-ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för skapandebegäran för en datauppsättning. | Datauppsättnings-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Tidsstämpel för senaste begäran om att skapa post för en datauppsättning. | Datauppsättnings-ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Frekvens för inaktuella tidsstämplade poster för uppdateringsbegäran för en datauppsättning. | Datauppsättnings-ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Tidsstämpel för senaste begäran om uppdatering av post för en datauppsättning. | Datauppsättnings-ID |
| platform.ups.ingest.streaming.record.size.m1_rate | Genomsnittlig poststorlek. | IMS-organisation |
| platform.ups.ingest.streaming.records.updated.m15_rate | Frekvens för uppdateringsbegäranden för poster som har importerats för en datauppsättning. | Datauppsättnings-ID |
