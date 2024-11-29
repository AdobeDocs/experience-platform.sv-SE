---
title: Real-time Customer Data Platform Insights - datamodell B2B edition
description: Lär dig hur du använder SQL-frågor med Real-time Customer Data Platform Insights Data Models (B2B edition) för att anpassa dina egna Real-Time CDP-rapporter för din marknadsföring och dina KPI-användningsfall.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Real-Time CDP Insights datamodell B2B edition

Real-Time CDP Insights-datamodellen för B2B edition visar de datamodeller och SQL som stöder insikterna för [kontoprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Du kan anpassa de här SQL-frågemallarna för att skapa Real-Time CDP-rapporter för användning av B2B-marknadsföring och KPI-indikatorer. Dessa insikter kan sedan användas som anpassade widgetar för dina instrumentpaneler.

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Real-Time CDP Prime- och Ultimate-paketet. Mer information finns i dokumentationen om [Real-Time CDP-utgåvorna](../../rtcdp/overview.md#rtcdp-editions), eller kontakta din Adobe-representant.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Förhandskrav

Den här handboken kräver en fungerande förståelse av anpassade instrumentpaneler. Läs dokumentationen om [hur du skapar en anpassad kontrollpanel](../standard-dashboards.md) innan du fortsätter med den här guiden.

## Real-Time CDP B2B-rapporter och användningsexempel {#B2B-insight-reports-and-use-cases}

Real-Time CDP B2B-rapportering ger insikter i era kontoprofiler och relationen mellan konton och affärsmöjligheter. Följande stjärnschemamodeller utvecklades för att besvara en rad vanliga användningsfall för marknadsföring, och varje datamodell kan stödja flera användningsfall.

>[!IMPORTANT]
>
>De data som används för Real-Time CDP B2B-rapportering är korrekta för en vald sammanfogningsprincip och från den senaste ögonblicksbilden.

### Kontoprofilmodell {#account-profile-model}

Kontoprofilmodellen består av åtta datauppsättningar:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

I diagrammet nedan visas de relevanta datafälten i varje datauppsättning, deras datatyp och de sekundärnycklar som länkar samman datauppsättningarna.

![Entitetsrelationsdiagrammet för kontoprofilmodellen.](../images/data-models/account-profile-model.png)

#### De nya kontona efter bransch {#accounts-by-industry}

Logiken som används för insikten [!UICONTROL New accounts by industry] returnerar de fem främsta branscherna utifrån deras antal kontoprofiler och deras relativa storlek till varandra. Mer information finns i [[!UICONTROL New accounts By Industry]-widgetens dokumentation ](../guides/account-profiles.md#accounts-by-industry).

>[!TIP]
>
>Du kan anpassa den här SQL-frågan så att den returnerar mer eller mindre än de fem främsta branscherna.

Den SQL som genererar insikten [!UICONTROL New accounts by industry] visas i det infällbara avsnittet nedan.

+++SQL-fråga

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### De nya kontona efter typ av användningsfall {#accounts-by-type}

Logiken som används för insikten [!UICONTROL New accounts by type] returnerar den numeriska uppdelningen av konton efter typ. Denna insikt kan hjälpa till att vägleda affärsstrategier och -åtgärder, inklusive resursallokering och marknadsföringsstrategier. Mer information finns i [[!UICONTROL New accounts by type]-widgetens dokumentation ](../guides/account-profiles.md#accounts-by-type).

Den SQL som genererar insikten [!UICONTROL New accounts by type] visas i det infällbara avsnittet nedan.

+++SQL-fråga

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

### Möjlighetsmodell {#opportunity-model}

Affärsmöjlighetsmodellen består av sju datauppsättningar:

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

Diagrammet nedan visar de relevanta datafälten i varje datauppsättning.

![Entitetsrelationsdiagrammet för affärsmöjlighetsmodellen.](../images/data-models/opportunity-model.png)
