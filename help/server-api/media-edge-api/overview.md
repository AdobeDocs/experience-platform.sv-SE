---
keywords: Experience Platform;mediekant;populära ämnen;datumintervall
solution: Experience Platform
title: Media Edge API:er
description: Översikt över API:er för Media Edge.
source-git-commit: 4f60b00026a226aa6465b2c21b3c2198962a1e3b
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---


# Översikt över API för Media Edge

Media Edge-API:er bygger på Adobe Experience Platform (AEP) för att tillhandahålla data för mediespårning inom ramen för [XDM-scheman](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). För kunder som använder Media Analytics blir följande funktioner tillgängliga:

* Med [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en), kan kunderna få detaljerade detaljer om varaktighet, start och stopp för att utvärdera och kombinera för mediemätningar. Kunder som migrerar från Adobe Analytics har alla rapporteringsmått tillgängliga i CJA.

* Med [Adobe Real-time Customer Data Platform (RTCDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=sv), kan kunderna utöka sina realtidsprofiler med medieförbrukningsdata.

* Med [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en)kan kunderna optimera flerkanalskampanjer och automatisera resor med mediekonsumtionssignaler.


## Optimera dataflöden för mediespårning

Båda [Media Collection API:er](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) och Media Edge API:er tillhandahåller mediespårningsdata som RESTful-tjänster. Men att använda tjänsten Media Edge har följande fördelar:

* Det är det enklaste sättet att införliva XDM-scheman i dataflödet.

* Samtal dirigeras från en mediespelare direkt till [Experience Edge Platform Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Den spårar mediahändelser effektivt med ett minimum av serveröverskridande anrop.

I följande tabell visas en möjlig Adobe API-tjänst för olika medieanalysfall:

| Användningsfall | API-tjänst |
| -------- | ------ |
| AEP-lösning (CJA, RTDCP, AJO, etc.) | Media Edge |
| CDP + CJA | Media Edge |
| Adobe Analytics + AEP | Media Edge |
| Endast Adobe Analytics (spårning redan) | Media Collection |

>[!NOTE]
>
> API-tjänsten Media Collection för Analytics tar fortfarande emot XDM-data, men den är inte optimerad i den utsträckning som tjänsten Media Edge är. Beroende på vilka data som skickas från Media Player kan vissa data som bara används för analys även slussas via API-tjänsten för Media Edge.

I följande bild visas dataflödena för de två API-tjänsterna:


![Dataflöden för medieanalys](../assets/edge-api-dataflow.png)


Mer information om hur du använder Media Edge API:er finns i [Komma igång med dokumentation](getting-started.md).

Mer information om hur du arbetar med Platform Edge finns i [Installera Media Analytics med Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




