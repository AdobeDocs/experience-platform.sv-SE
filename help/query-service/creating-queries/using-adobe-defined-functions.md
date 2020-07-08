---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe-definierade funktioner
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Använda Adobe-definierade funktioner

En av Adobes stora differentierande faktorer är att de förstår upplevelsedata och vad kunderna behöver kunna göra med dessa data. Du kan använda den här förståelsen för att skapa hjälpfunktioner som gör jobbet enklare.

Det här dokumentet innehåller Adobes definierade funktioner (ADF) som stöder tre viktiga Analytics-aktiviteter:
- [Yrkesställning](#sessionization)
- [Attribuering](#attribution)
- [Sökvägsanalys](#pathing)

## Yrkesställning

Besöksgrupperingarna `SESS_TIMEOUT()` som finns i Adobe Analytics återges. Den utför en liknande tidsbaserad gruppering, men med anpassningsbara parametrar.

**Syntax:**

`SESS_TIMEOUT(timestamp, timeout_in_seconds) OVER ([partition] [order] [frame])`

**Returnerar:**

Struktur med fält `(timestamp_diff, num, is_new, depth)`

### Utforska radnivå `SESS_TIMEOUT()` och utdata

```sql
SELECT analyticsVisitor,
      session.is_new,
      session.timestamp_diff,
      session.num,
      session.depth
FROM  (
        SELECT endUserIDs._experience.aaid.id as analyticsVisitor,
        SESS_TIMEOUT(timestamp, 60 * 30)
        OVER (PARTITION BY endUserIDs._experience.aaid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
        FROM your_analytics_table
        WHERE _ACP_YEAR = 2018
      )
LIMIT 100;
```

![Bild](../images/queries/adobe-functions/sess-timeout.png)

### Skapa en ny trendrapport med besökare, sessioner och sidvisningar

```sql
SELECT
      date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
      COUNT(DISTINCT analyticsVisitor ) as Visitors,
      COUNT(DISTINCT analyticsVisitor || session.num ) as Sessions,
      SUM( PageViews ) as PageViews
FROM
    (
      SELECT
          timestamp,
          endUserIDs._experience.aaid.id as analyticsVisitor,
          SESS_TIMEOUT(timestamp, 60 * 30)
      OVER (PARTITION BY endUserIDs._experience.aaid.id
      ORDER BY timestamp
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS session,
          web.webPageDetails.pageviews.value as PageViews
      FROM your_analytics_table
      WHERE _ACP_YEAR = 2018
    )
GROUP BY Day 
ORDER BY Day DESC 
LIMIT 31;
```

![Bild](../images/queries/adobe-functions/trended-report.png)

## Attribuering

Attribution är det sätt på vilket ni fördelar mätvärden eller konverteringar som intäkter, order eller registreringar till era marknadsföringssatsningar.

I Adobe Analytics konfigureras attribueringsinställningar med variabler som eVars och genereras när data importeras.

Attribution ADFs found in Query Service allow those allokations to be defined and generated at query time.

I det här exemplet fokuseras på attribuering med sista-beröringen, men Adobe erbjuder även attribuering med första-beröringen.

>[!NOTE]
>
>Andra alternativ med timeout och händelsebaserad förfallotid är tillgängliga i framtida versioner av Query Service.

**Syntax:**

`ATTRIBUTION_LAST_TOUCH(timestamp, [channel_name], column) OVER ([partition] [order] [frame])`

**Returnerar:**

Struktur med fält `(value)`

### Utforska radnivåattribueringen

```sql
SELECT
  endUserIds._experience.aaid.id,
  _experience.analytics.customDimensions.evars.evar10 as MemberLevel,
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=4
LIMIT 50;
```

![Bild](../images/queries/adobe-functions/row-level-attribution.png)

### Skapa en fördelning av order efter nivå för senaste medlem (eVar10)

```sql
SELECT
  LastMemberLevel,
  SUM(Orders) as MemberLevelOrders
FROM 
(SELECT
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=4
)
GROUP BY LastMemberLevel 
ORDER BY MemberLevelOrders DESC
LIMIT 25;
```

![Bild](../images/queries/adobe-functions/last-member-level.png)

## Sökvägsanalys

Pathing hjälper till att förstå hur kunderna navigerar på er webbplats. Med hjälp av `NEXT()` - och `PREVIOUS()` ADF-filer är detta möjligt.

**Syntax:**

```
NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
```

**Returnerar:**

Struktur med fält `(value)`

### Markera den aktuella sidan och nästa sida

```sql
SELECT 
      endUserIds._experience.aaid.id,
      timestamp,
      web.webPageDetails.name,
      NEXT(web.webPageDetails.name, 1, true)
          OVER(PARTITION BY endUserIds._experience.aaid.id
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS next_pagename
FROM your_analytics_table
WHERE _ACP_YEAR=2018 
LIMIT 10;
```

![Bild](../images/queries/adobe-functions/select-current-page.png)

### Skapa en detaljrapport för de fem översta sidnamnen när sessionen påbörjas

```sql
  SELECT 
    PageName,
    PageName_2,
    PageName_3,
    PageName_4,
    PageName_5,
    SUM(PageViews) as PageViews
  FROM
    (SELECT
      PageName,
      NEXT(PageName, 1, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_2,
      NEXT(PageName, 2, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_3,
      NEXT(PageName, 3, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_4,
      NEXT(PageName, 4, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_5,
      PageViews,
      session.depth AS SessionPageDepth
    FROM
      (SELECT
        endUserIds._experience.aaid.id as VisitorID,
        timestamp,
        web.webPageDetails.pageviews.value AS PageViews,
        web.webPageDetails.name AS PageName,
        SESS_TIMEOUT(timestamp, 60 * 30) 
          OVER (PARTITION BY endUserIDs._experience.aaid.id 
                ORDER BY timestamp 
                ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
        AS session
      FROM your_analytics_table
      WHERE _ACP_YEAR=2018)
    )
  WHERE SessionPageDepth=1
  GROUP BY PageName, PageName_2, PageName_3, PageName_4, PageName_5
  ORDER BY PageViews DESC
  LIMIT 100;
```

![Bild](../images/queries/adobe-functions/create-breakdown-report.png)

