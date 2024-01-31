---
title: Destinationsinsikter
description: Upptäck den SQL som ger er målgruppsinsikter och använder dessa frågor för att generera anpassade insikter för att ytterligare utforska aktiveringen av data från Adobe Experience Platform.
source-git-commit: 3d5dd6300952409e2dddb32eb11547fb43a5feac
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 0%

---

# Målinsikter

De insikter som bygger på analysen av er datamodell gör era Adobe Real-time Customer Data Platform-data mer tillgängliga, begripliga och slagkraftiga för beslutsfattandet.

Förstå era målinsikter genom att använda den SQL som ligger till grund för dem och generera sedan egna insikter för att ytterligare utforska aktiveringen av data från Adobe Experience Platform till målplattformarna. Omvandla era rådata till nya användbara insikter genom att använda Real-Time CDP datamodell SQL som inspiration för att skapa frågor som passar just era affärsbehov.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI.  -->

Du kan använda följande insikter som en del av [Kontrollpanel för destinationer](../guides/destinations.md) eller en egen [användardefinierad kontrollpanel](../user-defined-dashboards.md). Se [anpassningsöversikt](../customize/overview.md) för instruktioner om hur du anpassar kontrollpanelen eller [skapa och redigera nya widgetar](../customize/custom-widgets.md) i widgetbiblioteket och [användardefinierad kontrollpanel](../user-defined-dashboards.md#create-widget).

## Aktiverade målgrupper {#activated-audiences}

Frågor som besvaras av den här insikten:

- Vad är det totala antalet aktiverade målgrupper som filtreras efter ett visst mål?
- Vad är antalet aktiverade målgrupper för varje mål?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Se [Dokumentation för widgeten Aktiverade målgrupper](../guides/destinations.md#activated-audiences) om du vill ha information om hur den här insikten ser ut och fungerar.

## Aktiverade målgrupper över alla destinationer {#activated-audiences-across-all-destinations}

Frågor som besvaras av den här insikten:

- Hur många målgrupper aktiveras över alla destinationer?
- Vad är det totala antalet aktiverade målgrupper?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Se [Dokumentation för aktiverad målgrupp över alla målwidgetar](../guides/destinations.md#activated-audiences-across-all-destinations) om du vill ha information om hur den här insikten ser ut och fungerar.

## Aktiva destinationer per målplattform {#active-destinations-by-destination-platform}

Frågor som besvaras av den här insikten:

- Hur många destinationer är aktiva?
- Hur ser de aktiva destinationerna ut efter målplattform?
- Vad är antalet aktiva destinationer uppdelat efter respektive målplattform?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Se [Dokumentation för aktiva destinationer efter målplattformswidget](../guides/destinations.md#active-destinations-by-destination-platform) om du vill ha information om hur den här insikten ser ut och fungerar.

## Trend för målgruppsstorlek {#audience-size-trend}

Frågor som besvaras av den här insikten:

- Hur har målgruppens storlek ändrats över tid, inklusive avvikelser för en målgrupp som har mappats till ett mål?
- Hur ser jag den övergripande trenden i målgruppsstorlek per mål under de angivna perioderna på 30 dagar, 90 dagar och 12 månader?
- Vilka är de viktigaste egenskaperna hos den målgrupp som bidrar till storleken, till exempel toppar för alla e-postmarknadsföringskampanjer?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Se [Widget för målgruppsstorlekstrend, dokumentation](../guides/destinations.md#audience-size-trend) om du vill ha information om hur den här insikten ser ut och fungerar.

## Gemensamma målgrupper {#common-audiences}

Frågor som besvaras av den här insikten:

- Vilka målgrupper är gemensamma mellan två olika destinationer?
- Hur många profiler har var och en av de gemensamma målgrupperna mellan två olika destinationer?
- Vilken är den största målgruppen som två destinationer är mappade till?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Se [Dokumentation för widgeten Vanliga målgrupper](../guides/destinations.md#common-audiences) om du vill ha information om hur den här insikten ser ut och fungerar.

## Målstatus {#destination-status}

Frågor som besvaras av den här insikten:

- Vilket är det totala antalet destinationer som har aktiverats för användning?
- Vilket är det totala antalet inaktiverade destinationer?
- Hur stor är procentandelen som delas mellan aktiverade och inaktiverade destinationer?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Se [Dokumentation för widgeten Målstatus](../guides/destinations.md#destination-status) om du vill ha information om hur den här insikten ser ut och fungerar.

## Antal destinationer {#destinations-count}

Frågor som besvaras av den här insikten:

- Hur många destinationer är konfigurerade för närvarande?
- Hur har det totala antalet destinationer ändrats över tid?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Se [Dokumentation för widgeten Antal destinationer](../guides/destinations.md#destinations-count) om du vill ha information om hur den här insikten ser ut och fungerar.

## Hälsa för mappade målgrupper {#mapped-audience-health}

Frågor som besvaras av den här insikten:

- Vilka målgrupper som är mappade till ett mål har betydande variationer de senaste 30 dagarna?
- Vilken är den senaste storleken för en mappad publik och om den har ändrats under den senaste månaden?
- Hur listar jag alla målgrupper som är mappade till ett mål baserat på hur allvarlig deras storlek har ändrats den senaste månaden?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Se [Mappad dokumentation för målgruppens hälsowidget](../guides/destinations.md#mapped-audience-health) om du vill ha information om hur den här insikten ser ut och fungerar.

## Mappade målgrupper {#mapped-audiences}

Frågor som besvaras av den här insikten:

- Hur många målgrupper mappas till ett visst mål?
- Hur har antalet mappade målgrupper ändrats över tid?
- Var kan jag jämföra två destinationer för att se målgruppen överlappas av varje mål?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Se [Mappad målgruppswidget - dokumentation](../guides/destinations.md#mapped-audiences) om du vill ha information om hur den här insikten ser ut och fungerar.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Mest använda destinationer {#most-used-destinations}

Frågor som besvaras av den här insikten:

- Vilka är de vanligaste destinationerna?
- Hur många målgrupper mappas till varje mål, sorterat efter de flesta i alla fall?
- Hur ändras mappningen av målgrupper till mål från en ögonblicksbild till en annan?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Se [Dokumentation för den mest använda målwidgeten](../guides/destinations.md#most-used-destinations) om du vill ha information om hur den här insikten ser ut och fungerar.

## Nyligen aktiverade målgrupper {#recently-activated-audiences}

Frågor som besvaras av den här insikten:

- Vilken målgrupp aktiverades senast?
- Hur hittar jag en lista över alla destinationer sorterade efter det senaste uppdateringsdatumet?
- Hur kan jag jämföra två mål baserat på de senaste aktiveringarna?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Se [Dokumentation för widgeten Nyligen aktiverade målgrupper](../guides/destinations.md#recently-activated-audiences) om du vill ha information om hur den här insikten ser ut och fungerar.

## Nyligen aktiverade målgrupper efter mål {#recently-activated-audiences-by-destination}

Frågor som besvaras av den här insikten:

- Vilka målgrupper aktiveras för ett visst mål?
- Hur hittar jag en lista över målgrupper som aktiverats av en viss målgrupp från de flesta till de senaste?
- Hur hittar jag en lista över målgrupper efter det datum då den aktiverades för ett specifikt mål?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Se [Dokumentation om den senast aktiverade målgruppen efter målwidget](../guides/destinations.md#recently-activated-audiences-by-destination) om du vill ha information om hur den här insikten ser ut och fungerar.

## Nyligen skapade mål {#recently-created-destinations}

Frågor som besvaras av den här insikten:

- Vilka är de senast skapade destinationerna?
- Hur hittar jag en lista över destinationer med det datum då de skapades?
- Vilken ny destination skapades nyligen?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Se [Dokumentation för den senast skapade målwidgeten](../guides/destinations.md#recently-created-destinations) om du vill ha information om hur den här insikten ser ut och fungerar.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Nästa steg {#next-steps}

Genom att läsa det här dokumentet förstår du nu vilken SQL-kod som genererar instrumentpanelsinsikter och vilka vanliga frågor som analysen löser. Nu kan du redigera och iterera igenom dessa SQL-frågor för att generera egna insikter.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI. -->

Du kan även läsa och förstå den SQL som genererar insikter för [Profiler](./profiles.md) och [Målgrupper](./audiences.md) instrumentpaneler.

<!-- 
SQL MISSING FROM WIKI:
Unmapped audiences by identity
Mapped audiences by identity 
-->
