---
keywords: Experience Platform;home;populära topics;query service;Query service;experience event queries;experience event query;Experience Event query;
title: Visa en användares sidvyer
description: Lär dig hur du skriver frågor som använder Experience Events för att skapa en lista över de 100 senaste sidorna som en angiven användare har använt.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Visa en användares sidvyer

Det här dokumentet innehåller ett exempel på den SQL som krävs för att lista sidvyerna för en viss användare. Med Adobe Experience Platform Query Service kan du skriva frågor som använder [!DNL Experience Events] för att ta en mängd olika användningsområden. Experience Events representeras av Experience Data Model (XDM) ExperienceEvent-klassen, som fångar en oföränderlig och icke-aggregerad ögonblicksbild av systemet när en användare interagerar med en webbplats eller tjänst. Experience Events kan till och med användas för tidsdomänanalys. Se [nästa steg](#next-steps) för fler användningsfall där [!DNL Experience Events] för att generera besökarrapporter.

Mer information om XDM och [!DNL Experience Events] finns i [[!DNL XDM System] översikt](../../xdm/home.md). Genom att kombinera frågetjänsten med [!DNL Experience Events]kan ni effektivt spåra beteendetrender bland era användare. Följande dokument innehåller exempel på frågor som innehåller [!DNL Experience Events].

## Syfte

I följande exempel visas de 100 senaste sidorna som en angiven användare har visat.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Resultatet av den här frågan visas nedan.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du en bättre förståelse för hur du använder frågetjänsten med [!DNL Experience Events] för att lista sidvyerna som en angiven användare.

Läs följande användningsexempel om du vill veta mer om andra besöksbaserade användningsfall:

- [Hämta en lista med besökare ordnade efter antal sidvisningar.](./visitors-by-number-of-page-views.md)
- [Visa en sammanställningsrapport för en besökare.](./roll-up-report-of-a-visitor.md)
- [Skapa en trendrapport över händelser per dag.](./trended-report-of-events.md)
