---
keywords: Experience Platform;home;populära topics;query service;Query service;experience event queries;experience event query;Experience Event query;
title: Skapa en trendrapport över händelser
description: Lär dig hur du skriver frågor som använder Experience Events för att skapa en trendrapport med händelser över ett visst datumintervall, grupperade efter datum.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# Skapa en trendrapport över händelser

Det här dokumentet innehåller ett exempel på den SQL som krävs för att skapa en trendrapport över händelser per dag i ett visst datumintervall. Med Adobe Experience Platform Query Service kan du skriva frågor som använder [!DNL Experience Events] för att ta en mängd olika användningsområden. Experience Events representeras av Experience Data Model (XDM) ExperienceEvent-klassen, som fångar en oföränderlig och icke-aggregerad ögonblicksbild av systemet när en användare interagerar med en webbplats eller tjänst. Experience Events kan till och med användas för tidsdomänanalys. Se [nästa steg](#next-steps) för fler användningsfall där [!DNL Experience Events] för att generera besökarrapporter.

Rapporterna ger er tillgång till era plattformsdata för att hjälpa er organisations strategiska affärsinsikter. Med de här rapporterna kan ni undersöka era plattformsdata på flera olika sätt, visa nyckeltal i lättbegripliga format och dela de insikter de ger.

Mer information om XDM och [!DNL Experience Events] finns i [[!DNL XDM System] översikt](../../xdm/home.md). Genom att kombinera frågetjänsten med [!DNL Experience Events]kan ni effektivt spåra beteendetrender bland era användare. Följande dokument innehåller exempel på frågor som innehåller [!DNL Experience Events].

## Mål

I följande exempel skapas en trendrapport med händelser över ett angivet datumintervall grupperade efter datum. Det här SQL-exemplet sammanfattar olika analysvärden som `A`, `B`och `C`och sammanfattar sedan antalet gånger som parkas har visats under en månad.

Tidsstämpelkolumnen finns i [!DNL Experience Event] datauppsättningar har UTC-format. Exemplet använder `from_utc_timestamp()` för att omforma tidsstämpeln från UTC till EDT och sedan använder `date_format()` för att isolera datumet från resten av tidsstämpeln.

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
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
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

Resultatet av den här frågan visas nedan.

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du en bättre förståelse för hur du använder frågetjänsten med [!DNL Experience Events] för att effektivt spåra beteendetrender bland era användare.

Så här lär du dig mer om andra besöksbaserade användningsfall som använder [!DNL Experience Events]kan du läsa följande dokument:

- [Hämta en lista med besökare ordnade efter antal sidvisningar.](./visitors-by-number-of-page-views.md)
- [Visa en besökares tidigare sessioner.](./list-visitor-sessions.md)
- [Visa en sammanställningsrapport för en besökare.](./roll-up-report-of-a-visitor.md)
