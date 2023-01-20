---
title: Real-time Customer Data Platform Insights-datamodell
description: Lär dig hur du använder SQL-frågor med Real-time Customer Data Platform Insights-datamodeller för att anpassa dina egna Real-Time CDP-rapporter för din marknadsföring och dina KPI-användningsfall.
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Real-time Customer Data Platform Insights-datamodell

Funktionen Real-time Customer Data Platform Insights-datamodell visar de datamodeller och SQL som används för insikter om olika profil-, mål- och segmenteringswidgetar. Du kan anpassa dessa SQL-frågemallar för att skapa Real-Time CDP-rapporter för dina KPI-fall (Marketing and Key Performance Indicator). Dessa insikter kan sedan användas som anpassade widgetar för dina användardefinierade instrumentpaneler. Läs dokumentet med information om rapportinsikter i det accelererade arkivet om du vill veta mer [hur man bygger en datamodell med rapportinsikter med hjälp av frågetjänsten för användning med accelererade lagringsdata och användardefinierade instrumentpaneler](../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md).

## Förutsättningar

Den här guiden kräver en fungerande förståelse av [användardefinierad panelfunktion](./user-defined-dashboards.md). Läs dokumentationen innan du fortsätter med den här guiden.

## Real-Time CDP insiktsrapporter och användningsexempel

Real-Time CDP rapportering ger insikter i era profildata och dess relation till segment och destinationer. Olika stjärnschemamodeller utvecklades för att besvara en rad vanliga användningsfall för marknadsföring, och varje datamodell kan stödja flera användningsfall.

>[!IMPORTANT]
>
>De data som används för Real-Time CDP-rapportering är korrekta för en vald sammanfogningsprincip och från den senaste ögonblicksbilden.

### Profilmodell {#profile-model}

Profilmodellen består av tre datauppsättningar:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för profilmodellen.](./images/cdp-insights/profile-model.png)

#### Användningsfall för antal profiler

Den logik som används för widgeten för antal profiler returnerar det totala antalet sammanfogade profiler i profilarkivet när ögonblicksbilden togs. Se [[!UICONTROL Profile count] widgetdokumentation](./guides/profiles.md#profile-count) för mer information.

Den SQL som genererar [!UICONTROL Profile count] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Enstaka identitetsprofiler använder sig av gemener/versaler

Den logik som används för [!UICONTROL Single identity profiles] widgeten innehåller ett antal profiler för din organisation som bara har en typ av ID-typ som skapar deras identitet. Se[[!UICONTROL Single identity profiles] widgetdokumentation](./guides/profiles.md#single-identity-profiles) för mer information.

Den SQL som genererar [!UICONTROL Single identity profiles] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### Namnområdesmodell {#namespace-model}

Namnområdesmodellen består av följande datamängder:

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för namnutrymmesmodellen.](./images/cdp-insights/namespace-model.png)

#### Profiler efter användningsfall för identitet

The [!UICONTROL Profiles by identity] widgeten visar en beskrivning av identiteterna för alla sammanfogade profiler i din profilbutik. Se [[!UICONTROL Profiles by identity] widgetdokumentation](./guides/profiles.md#profiles-by-identity) för mer information.

Den SQL som genererar [!UICONTROL Profiles by identity] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### Enstaka identitetsprofiler efter användningsfall för identitet

Den logik som används för [!UICONTROL Single identity profiles by identity] visar det totala antalet profiler som identifieras med endast en unik identifierare. Se [Dokumentation för en identitetsprofil per identitetswidget](./guides/profiles.md#single-identity-profiles-by-identity) för mer information.

Den SQL som genererar [!UICONTROL Single identity profiles by identity] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### Segmentmodell {#segment-model}

Segmentmodellen består av följande datamängder:

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för segmentmodellen.](./images/cdp-insights/segment-model.png)

#### Målgruppsstorlek - skiftläge

Den logik som används för [!UICONTROL Audience size] returnerar det totala antalet sammanfogade profiler i det markerade segmentet vid tidpunkten för den senaste ögonblicksbilden. Se [[!UICONTROL Audience size] widgetdokumentation](./guides/segments.md#audience-size) för mer information.

Den SQL som genererar [!UICONTROL Audience size] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### Trend för ändring av målgruppsstorlek - skiftläge

Den logik som används för [!UICONTROL Audience size change trend] visar en graf för en linje som visar skillnaden i det totala antalet profiler som är kvalificerade för ett visst segment mellan de senaste ögonblicksbilderna. Se [[!UICONTROL Audience size change trend] widgetdokumentation](./guides/segments.md#audience-size-change-trend) för mer information.

Den SQL som genererar [!UICONTROL Audience size change trend] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### De flesta destinationer använder versaler

Den logik som används i [!UICONTROL Most used destinations] widgeten visar organisationens mest använda mål baserat på antalet segment som mappats till dem. Denna rankning ger insikt i vilka destinationer som används samtidigt som de som kan vara underutnyttjade också kan visas. Läs dokumentationen på [[!UICONTROL Most used destinations] widget](./guides/destinations.md#most-used-destinations) för mer information.

Den SQL som genererar [!UICONTROL Most used destinations] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### Nyligen aktiverade segment - användningsfall

Logiken i [!UICONTROL Recently activated segments] widgeten innehåller en lista med de segment som senast har mappats till ett mål. Den här listan innehåller en ögonblicksbild av de segment och mål som används aktivt i systemet och kan hjälpa till att felsöka felaktiga mappningar. Se [[!UICONTROL Recently activated segments] widgetdokumentation](./guides/destinations.md#recently-activated-segments) för mer information.

Den SQL som genererar [!UICONTROL Recently activated segments] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### Namespace-segment model

Namnutrymmessegmentmodellen består av följande datamängder:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för namnutrymmessegmentsmodellen.](./images/cdp-insights/namespace-segment-model.png)

#### Profiler per identitet för ett segmentanvändningsfall

Den logik som används i [!UICONTROL Profiles by identity] widgeten innehåller en beskrivning av identiteterna för alla sammanfogade profiler i din profilbutik för ett visst segment. Se [[!UICONTROL Profiles by identity] widgetdokumentation](./guides/segments.md#profiles-by-identity) för mer information.

Den SQL som genererar [!UICONTROL Profiles by identity] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### Överlappa namnutrymmesmodell

Den överlappande namnområdesmodellen består av följande datamängder:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för den överlappande namnutrymmesmodellen.](./images/cdp-insights/overlap-namespace-model.png)

#### Användningsfall för identitetsöverlappning (profiler)

Den logik som används i [!UICONTROL Identity overlap] widgeten visar överlappningen av profiler i **Profilarkiv** som innehåller de två markerade identiteterna. Mer information finns i [[!UICONTROL Identity overlap] widgetavsnitt i [!UICONTROL Profiles] dokumentation för kontrollpanelen](./guides/profiles.md#identity-overlap).

Den SQL som genererar [!UICONTROL Identity overlap] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### Överlappa namnutrymme efter segmentmodell

Namnutrymmet för överlappning efter segmentmodell består av följande datamängder:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Bilden nedan innehåller de relevanta datafälten i varje datauppsättning.

![En ERD för det överlappande namnutrymmet efter segmentmodell.](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### Användningsfall för identitetsöverlappning (segment)

Den logik som används i [!UICONTROL Segments] kontrollpanel [!UICONTROL Identity overlap] widgeten visar överlappningen av profiler som innehåller de två valda identiteterna för ett visst segment. Mer information finns i [[!UICONTROL Identity overlap] widgetavsnitt i [!UICONTROL Segmentation] dokumentation för kontrollpanelen](./guides/segments.md#identity-overlap).

Den SQL som genererar [!UICONTROL Identity overlap] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
