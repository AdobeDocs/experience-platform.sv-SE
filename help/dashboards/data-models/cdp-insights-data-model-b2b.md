---
title: Real-time Customer Data Platform Insights - datamodell B2B Edition
description: Lär dig hur du använder SQL-frågor med Real-time Customer Data Platform Insights-datamodeller (B2B Edition) för att anpassa dina egna Real-Time CDP-rapporter för din marknadsföring och dina KPI-användningsfall.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 52f67037756af97bac97908d4736a3cbafce6844
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Real-time Customer Data Platform Insights, datamodell B2B Edition

Datamodellen Real-time Customer Data Platform Insights för B2B Edition visar de datamodeller och SQL som ligger till grund för insikterna för [kontoprofiler](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Du kan anpassa de här SQL-frågemallarna för att skapa Real-Time CDP-rapporter för användning av B2B-marknadsföring och KPI-indikatorer. Dessa insikter kan sedan användas som anpassade widgetar för dina instrumentpaneler.

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Real-Time CDP Prime- och Ultimate-paketet. Se dokumentationen om [Real-Time CDP editions](../../rtcdp/overview.md#rtcdp-editions) om du vill ha mer information eller kontakta din Adobe-representant.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md).
 -->

## Förutsättningar

Den här handboken kräver en fungerande förståelse av anpassade instrumentpaneler. Läs dokumentationen på [hur du skapar en anpassad kontrollpanel](../user-defined-dashboards.md) innan du fortsätter med den här guiden.

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

#### Användningsexempel för konton efter bransch {#accounts-by-industry}

Den logik som används för [!UICONTROL Accounts By Industry] insight returnerar de fem främsta branscherna utifrån deras antal kontoprofiler och deras relativa storlek till varandra. Se [[!UICONTROL Accounts By Industry] widgetdokumentation](../guides/account-profiles.md#accounts-by-industry) för mer information.

>[!TIP]
>
>Du kan anpassa den här SQL-frågan så att den returnerar mer eller mindre än de fem främsta branscherna.

Den SQL som genererar [!UICONTROL Accounts By Industry] finns i det infällbara avsnittet nedan.

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

#### Användningsexempel för konton efter typ {#accounts-by-type}

Den logik som används för [!UICONTROL Accounts By Type] insight returnerar den numeriska uppdelningen av konton efter typ. Denna insikt kan hjälpa till att vägleda affärsstrategier och -åtgärder, inklusive resursallokering och marknadsföringsstrategier. Se [[!UICONTROL Accounts By Type] widgetdokumentation](../guides/account-profiles.md#accounts-by-type) för mer information.

Den SQL som genererar [!UICONTROL Accounts By Type] finns i det infällbara avsnittet nedan.

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
