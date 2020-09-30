---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Sammanfoga datauppsättningar
topic: queries
type: Tutorial
description: Genom att koppla datauppsättningar kan du inkludera data från andra datauppsättningar i din fråga. I det här exemplet används en anpassad datamängd för operativsystem för att mappa operatorsystemID till operativsystemsvärdet.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

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
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Bild](../images/queries/joining-datasets/select-operating-systems.png)