---
keywords: Experience Platform;home;populära topics;query service;Query service;experience event queries;experience event query;Experience Event query;
title: Visa en sammanslagningsrapport för en specifik besökare
description: Följande dokument innehåller exempel på frågor som innehåller Experience Events i Adobe Experience Platform Query Service.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Visa en sammanslagningsrapport för en specifik besökare

Det här dokumentet innehåller ett SQL-exempel som används för att samla data från flera analysegenskaper för en viss användare och se dessa data tillsammans i en rapport. Med Adobe Experience Platform Query Service kan du skriva frågor som använder [!DNL Experience Events] för att ta en mängd olika användningsområden. Experience Events representeras av Experience Data Model (XDM) ExperienceEvent-klassen, som fångar en oföränderlig och icke-aggregerad ögonblicksbild av systemet när en användare interagerar med en webbplats eller tjänst. Experience Events kan till och med användas för tidsdomänanalys. Se [nästa steg](#next-steps) för fler användningsfall där [!DNL Experience Events] för att generera besökarrapporter.

Mer information om XDM och [!DNL Experience Events] finns i [[!DNL XDM System] översikt](../../xdm/home.md). Genom att kombinera frågetjänsten med [!DNL Experience Events]kan ni effektivt spåra beteendetrender bland era användare. Följande dokument innehåller exempel på frågor som innehåller [!DNL Experience Events].

## Syfte

I följande SQL-exempel visas hur du visar en sammanställd rapport med olika analysvärden för en angiven användare.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

Frågeresultaten visas i tabellen nedan.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du en bättre förståelse för hur du använder frågetjänsten med [!DNL Experience Events] om du vill visa en sammanställd rapport med analysvärden för en angiven användare.

Läs följande användningsexempel om du vill veta mer om andra besöksbaserade användningsfall:

- [Hämta en lista med besökare ordnade efter antal sidvisningar.](./visitors-by-number-of-page-views.md)
- [Visa en besökares tidigare sessioner.](./list-visitor-sessions.md)
- [Skapa en trendrapport över händelser per dag.](./trended-report-of-events.md)
