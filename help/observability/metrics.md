---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tillgängliga mått
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Lista över tillgängliga mätvärden

Nedan finns en lista över mätvärden som visas av observabilitetsinsikter, var och en med tillhörande plattformstjänst, beskrivning och accepterad ID-frågeparameter.

| Insikter - mått | Plattformstjänst | Beskrivning | ID-frågeparameter |
| ---- | ---- | ---- | ---- |
| timeseries.inghit.dataset.new.count | Dataintag | Totalt antal datauppsättningar som skapats. | Ej tillämpligt |
| timeseries.inghit.dataset.size | Dataintag | Kumulativ storlek för alla data som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.inghit.dataset.dailysize | Dataintag | Storlek på data som hämtas dagligen för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.inghit.dataset.batchfailed.count | Dataintag | Antal misslyckade batchar för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.inghit.dataset.batchsuccess.count | Dataintag | Antal batchar som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.inghit.dataset.recordsuccess.count | Dataintag | Antal poster som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.total.messages.rate | Dataintag (direktuppspelning) | Totalt antal meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.valid.messages.rate | Dataintag (direktuppspelning) | Totalt antal giltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.invalid.messages.rate | Dataintag (direktuppspelning) | Totalt antal ogiltiga meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.type.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga typmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.range.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga intervallmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.format.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga formatmeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.pattern.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga mönstermeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.presence.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga närvaromeddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.enum.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga enum-meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.unclassified.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga oklassificerade meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.validation.category.unknown.count | Dataintag (direktuppspelning) | Totalt antal ogiltiga &quot;okända&quot; meddelanden för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.data.collection.inlet.total.messages.receive | Dataintag (direktuppspelning) | Totalt antal meddelanden som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID (valfritt) |
| timeseries.data.collection.inlet.total.messages.size.receive | Dataintag (direktuppspelning) | Total storlek på data som tagits emot för ett dataintag eller för alla datainmatningar. | Intag-ID (valfritt) |
| timeseries.data.collection.inlet.success | Dataintag (direktuppspelning) | Totalt antal lyckade HTTP-anrop till ett dataintag eller till alla datainmatningar. | Intag-ID (valfritt) |
| timeseries.data.collection.inlet.error | Dataintag (direktuppspelning) | Totalt antal misslyckade HTTP-anrop till en datainmatning eller till alla datainmatningar. | Intag-ID (valfritt) |
| timeseries.profiles.dataset.recordread.count | Kundprofil i realtid | Antal poster som har lästs från datasjön efter profil, för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.recordsuccess.count | Kundprofil i realtid | Antal poster skrivna till datakällan per profil, för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.recordfailed.count | Kundprofil i realtid | Antal poster som misslyckades av profilen, för en datamängd eller för alla datamängder. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.batchsuccess.count | Kundprofil i realtid | Antal profilgrupper som har importerats för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.profiles.dataset.batchfailed.count | Kundprofil i realtid | Antal misslyckade profilbatchar för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.identity.dataset.recordsuccess.count | Identitetstjänst | Antal poster som skrivits till datakällan av identitetstjänsten, för en datauppsättning eller alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.identity.dataset.recordfailed.count | Identitetstjänst | Antal poster som misslyckades av identitetstjänsten, för en datauppsättning eller för alla datauppsättningar. | Datauppsättnings-ID (valfritt) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Identitetstjänst | Antal identitetsposter som har importerats för ett namnområde. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Identitetstjänst | Antal Identity-poster som misslyckades av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Identitetstjänst | Antal Identitetsposter som hoppats över av ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imfort.uniqueidentities.count | Identitetstjänst | Antal unika identiteter som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imugger.namespacecode.uniqueidentities.count | Identitetstjänst | Antal unika identiteter som lagras i identitetsdiagrammet för ett namnutrymme. | Namnområdes-ID (**obligatoriskt**) |
| timeseries.identity.graph.imugger.numidgraphs.count | Identitetstjänst | Antal unika diagramsymboler som lagras i identitetsdiagrammet för din IMS-organisation. | Ej tillämpligt |
| timeseries.identity.graph.imugger.graphstrength.uniqueidentities.count | Identitetstjänst | Antal unika identiteter som lagras i identitetsdiagrammet för IMS-organisationen för en viss grafikstyrka (&quot;unknown&quot;,&quot;svag&quot; eller&quot;strong&quot;). | Diagramstyrka (**krävs**) |
| timeseries.gdpr.job.totaljob.count | GDPR | Totalt antal jobb skapade från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.job.complete.job.count | GDPR | Totalt antal slutförda jobb från GDPR. | ENV (**obligatoriskt**) |
| timeseries.gdpr.job.errorjob.count | GDPR | Totalt antal feljobb från GDPR. | ENV (**obligatoriskt**) |
| timeseries.queryservice.query.eduleonce.count | Frågetjänst | Totalt antal icke återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.eduledåterkommande.count | Frågetjänst | Totalt antal återkommande schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchquery.count | Frågetjänst | Totalt antal utförda gruppfrågor. | Ej tillämpligt |
| timeseries.queryservice.query.eduledquery.count | Frågetjänst | Totalt antal utförda schemalagda frågor. | Ej tillämpligt |
| timeseries.queryservice.query.interactive.query.count | Frågetjänst | Totalt antal utförda interaktiva frågor. | Ej tillämpligt |
| timeseries.queryservice.query.batchfrompsqlquery.count | Frågetjänst | Totalt antal utförda batchfrågor från PSQL. | Ej tillämpligt |