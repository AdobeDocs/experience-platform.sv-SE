---
title: Kontoprofilsinsikter
description: Upptäck den SQL som ger er insikter om er kontoprofil och använd dessa frågor för att generera anpassade insikter som ytterligare utforskar era kunder och deras kundupplevelser.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# Kontoprofilsinsikter

[Kontoprofiler](../../rtcdp/accounts/account-profile-overview.md) används för att konsolidera kontoinformation från olika källor, inklusive flera marknadsföringskanaler och organisationssystem. Denna enhetliga vy ger en heltäckande bild av kundkonton och förbättrar B2B-marknadsföringskampanjer. De insikter som bygger på analysen av er datamodell gör era Adobe Real-time Customer Data Platform B2B-data mer tillgängliga, begripliga och effektiva för beslutsfattande.

Med tillgång till den SQL som ger er insikt kan ni bättre förstå era B2B-data och generera egna anpassningsbara återanvändbara insikter för att ytterligare utforska kundkontoinformationen. Omvandla era rådata till nya användbara insikter genom att använda Real-Time CDP datamodell SQL som inspiration för att skapa frågor som passar just era affärsbehov.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Följande insikter är tillgängliga för dig att använda som en del av kontrollpanelen [Kontoprofiler](../guides/account-profiles.md) eller en [anpassad kontrollpanel](../user-defined-dashboards.md). Se [anpassningsöversikten](../customize/overview.md) för instruktioner om hur du anpassar din instrumentpanel eller [skapar och redigerar nya widgetar](../customize/custom-widgets.md) i widgetbiblioteket och [användardefinierad instrumentpanel](../user-defined-dashboards.md#create-widget).

## Kontoprofiler har lagts till {#account-profiles-added}

Frågor som besvaras av den här insikten:

- Hur många kontoprofiler har lagts till under en viss period?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Nya konton efter bransch {#accounts-by-industry}

Frågor som besvaras av den här insikten:

- Vilka är de fem viktigaste branscherna som kontoprofilerna tillhör?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Nya konton efter typ {#accounts-by-type}

Frågor som besvaras av den här insikten:

- Vad är antalet konton efter typ?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## Möjligheter har lagts till {#opportunities-added}

Frågor som besvaras av den här insikten:

- Hur många möjligheter har lagts till under en viss period?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Nya möjligheter per personroll {#opportunities-by-person-role}

Frågor som besvaras av den här insikten:

- Vilken är den relativa storleken och antalet av de olika rollerna i en affärsmöjlighet?

+++Välj för att visa den SQL som genererar den här insikten

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Nya möjligheter per intäkt {#opportunities-by-revenue}

Frågor som besvaras av den här insikten:

- Vilka är de 20 främsta möjligheterna som rankas av deras intäkter (i USD)?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Nya möjligheter per status och fas {#opportunities-by-status-and-stage}

Frågor som besvaras av den här insikten:

- Vilka öppna möjligheter finns det och i vilket skede av försäljnings- eller marknadsföringstratten finns det?
- Vilka stängda möjligheter finns det och i vilket skede av försäljnings- eller marknadsföringstratten är de?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Nya möjligheter {#opportunities-won}

Frågor som besvaras av den här insikten:

- Hur många möjligheter har stängts eller slutförts?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Vunna affärsmöjligheter (linjediagram) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Frågor som besvaras av den här insikten:

- Hur många möjligheter har stängts eller slutförts (vunnits) under en viss period?

+++Välj för att visa den SQL som genererar den här insikten

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Nästa steg

Genom att läsa det här dokumentet förstår du nu vilken SQL som genererar insikter om kontrollpanelen för kontoprofiler och vilka vanliga frågor som analysen löser. Nu kan du redigera och iterera på SQL för att generera egna insikter.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

Du kan också läsa och förstå SQL-koden som genererar insikter för kontrollpanelerna [Profiler](./profiles.md), [Publiker](./audiences.md) och [Destinationer](./destinations.md).
