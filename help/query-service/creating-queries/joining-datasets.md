---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sammanfoga datauppsättningar
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 0%

---


# Sammanfoga datauppsättningar

Genom att koppla datauppsättningar kan du inkludera data från andra datauppsättningar i din fråga. I det här exemplet används en anpassad datamängd för operativsystem för att mappa `operatingsystemID` till `operatingsystem` värdet.

Datauppsättningar:
- your_analytics_table
- custom_operating_system_lookup

Skapa en `SELECT` programsats för de 50 främsta operativsystemen efter antal sidvisningar.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Bild](../images/queries/joining-datasets/select-operating-systems.png)