---
title: Aktivitetsanalys med Adobe Target
description: I det här dokumentet beskrivs hur du använder frågetjänsten för att skapa åtgärdbara insikter från datauppsättningar som har skapats med dina Adobe Target-data.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Aktivitetsanalys med Adobe Target

Med Adobe Experience Platform kan du importera data från Adobe Target med hjälp av XDM-fält (Experience Data Model) för att skapa datauppsättningar som kan användas med Query Service. Eftersom Adobe Target är utformat för att anpassa innehåll och personalisera användarupplevelser, kan frågor som körs på dessa datauppsättningar ge högpersonaliserade och fokuserade insikter genom att analysera användaraktivitet via SQL.

Det här dokumentet innehåller ett antal exempel på SQL-frågor som visar vanliga användningsfall baserat på kundernas beteenden och egenskaper.

## Komma igång

För vart och ett av följande användningsfall anges ett parametriserat SQL-frågeexempel som en mall som du kan anpassa. Ange parametrar var du än ser `{ }` i de SQL-exempel som du är intresserad av att utvärdera.

## Partiell XDM-fältmappning på hög nivå

I följande tabell visas vanliga målfält och motsvarande XDM-fält som de mappar till.

>[!NOTE]
>
>Användning av `[ ]` i XDM-fältet betecknar en array.

| Namn på målfält | XDM-fältnamn | Anteckningar |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | Ej tillämpligt |
| Aktivitets-ID | `_experience.target.activities.activityID` | Ej tillämpligt |
| Experience ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | Ej tillämpligt |
| Segment-ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | Ej tillämpligt |
| Händelseomfång | `_experience.target.activities[].activityEvents[].eventScope` | Det här fältet spårar nya besökare och besök. |
| Steg-ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Det här fältet är ett anpassat steg-ID för Adobe Campaign. |
| Prissumma | commerce.order.priceTotal | Ej tillämpligt |

>[!IMPORTANT]
>
>Namnet på en datauppsättning som skapas automatiskt med Target-data är&quot;Adobe Target Experience Events&quot;. Använd namnet när du använder den här datauppsättningen med frågor `adobe_target_experience_events`.

## Mål

Genom att analysera användaraktiviteter kan ni personalisera innehåll för en viss målgrupp och testa olika versioner av innehållet för en enskild enhet. Genom att analysera en viss aktivitet under en viss tidsperiod eller för enskilda användare kan dessutom resultatet för varje enskild aktivitet bli tydligare. Resultaten av den här kombinerade analysen kan användas för att förstå hur varje enskild aktivitet fungerar.

Följande användningsexempel för personalisering skapas med hjälp av Adobe Target-data och fokuserar på användaraktiviteter för att skapa värdefulla insikter om kundernas beteende framför affärsprogram.

Den här guiden illustrerar följande viktiga begrepp med exempel på användningsfall:

* För att förstå prestanda för ett aktivitets-ID för en viss dag, till exempel antal, detaljer och associerade upplevelse-ID:n.
* För att fastställa besökaren och händelseomfånget för en aktivitet.
* Om du vill samla in antalet besökare, besök och visningsinformation för Experience ID, Segment ID och Activity ID.

### Generera antal aktiviteter per timme för en given dag

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Generera timinformation för en viss

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Bestäm listan över upplevelse-ID:n för en specifik aktivitet för en given dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Returnera en lista med händelseomfång (besökare, besök, intryck) per instans per aktivitets-ID för en given dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Bestäm antalet besökare, besök och visningar per aktivitet för en viss dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Identifiera besökare, besök och visningar för Experience ID, Segment ID och EventScope för en viss dag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### Returnera mbox-namn och antal poster för en given dag

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
