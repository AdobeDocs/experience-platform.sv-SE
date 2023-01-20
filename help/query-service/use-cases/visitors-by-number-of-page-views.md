---
keywords: Experience Platform;home;populära topics;query service;Query service;experience event queries;experience event query;Experience Event query;
title: Visa besökare efter antal sidvisningar
description: Lär dig hur du skriver frågor som använder Experience Events för att hämta en lista över besökare ordnade efter antalet sidvisningar.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Visa besökarna efter deras antal sidvisningar

Det här dokumentet innehåller ett exempel på den SQL som krävs för att hämta en lista över besökare, ordnad efter antalet sidvisningar. Med Adobe Experience Platform Query Service kan du skriva frågor som använder [!DNL Experience Events] för att ta en mängd olika användningsområden. Experience Events representeras av Experience Data Model (XDM) ExperienceEvent-klassen, som fångar en oföränderlig och icke-aggregerad ögonblicksbild av systemet när en användare interagerar med en webbplats eller tjänst. Experience Events kan till och med användas för tidsdomänanalys. Se [nästa steg](#next-steps) för fler användningsfall där [!DNL Experience Events] för att generera besökarrapporter.

Mer information om XDM och [!DNL Experience Events] finns i [[!DNL XDM System] översikt](../../xdm/home.md). Genom att kombinera frågetjänsten med [!DNL Experience Events]kan ni effektivt spåra beteendetrender bland era användare. Följande dokument innehåller exempel på frågor som innehåller [!DNL Experience Events].

## Syfte

I följande exempel skapas en rapport som visar de 10 ID:n för de användare som har visat de flesta sidorna.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Frågeresultaten visas i tabellen nedan.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet får du en bättre förståelse för hur du använder frågetjänsten med [!DNL Experience Events] för att lista användare som har visat de flesta sidor.

Läs följande användningsexempel om du vill veta mer om andra besöksbaserade användningsfall:

- [Visa en besökares tidigare sessioner.](./list-visitor-sessions.md)
- [Visa en sammanställningsrapport för en besökare.](./roll-up-report-of-a-visitor.md)
- [Skapa en trendrapport över händelser per dag.](./trended-report-of-events.md)
