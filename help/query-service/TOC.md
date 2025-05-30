---
audience: user
user-guide-title: Hjälp med Adobe Experience Platform Query Service
breadcrumb-title: Användarhandbok om Query Service
user-guide-description: Använd standard-SQL för att fråga efter data i datasjön i Experience Platform.
feature: Queries
role: User,Developer
source-git-commit: 8b33d9231aeebd454fd614a81b356a9e971b757c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 14%

---


# Adobe Experience Platform Query Service {#query}

- [Översikt över frågetjänsten](home.md)
- [Paket för frågetjänst](packaging.md)
- [Skyddsutkast för frågetjänst](guardrails.md)
- Kom igång {#get-started}
   - [Förhandskrav](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Översikt](data-distiller/overview.md)
   - [Licensanvändning](data-distiller/license-usage.md)
   - Härledda datauppsättningar {#derived-datasets}
      - [Översikt](data-distiller/derived-datasets/overview.md)
      - [Skapa härledda datauppsättningar med SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Skapa decimalbaserade härledda datauppsättningar](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights för utökad apprapportering {#sql-insights}
      - [Översikt](data-distiller/sql-insights/overview.md)
      - [Frågepro-läge](data-distiller/sql-insights/query-pro-mode.md)
      - [Översikt över accelererad butik](data-distiller/sql-insights/accelerated-store-overview.md)
      - [Skicka accelererade frågor](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Datamodellguide för rapportinsikter](data-distiller/sql-insights/reporting-insights-data-model.md)
   - AI/ML-rörledningar {#ml-feature-pipelines}
      - [Översikt](data-distiller/ml-feature-pipelines/overview.md)
      - [Anslut till Jupyter-anteckningsböcker](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Förberedande dataanalys](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Teknikfunktioner för XML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportera data till ML-miljöer](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML-arbetsflöde för berikning av data från början till slut](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
   - [Summit 2025-sessionen](data-distiller/top-tips-to-maximize-value.md)
- Data, Distiller-statistik och maskininlärning {#advanced-statistics}
   - [Översikt](advanced-statistics/overview.md)
   - [Funktionsteknik](advanced-statistics/feature-engineering.md)
   - [Models](advanced-statistics/models.md)
   - [Omvandling av funktioner](advanced-statistics/feature-transformation.md)
   - Implementeringsmodeller {#implement-models}
      - [Implementeringsmodeller](advanced-statistics/implement-models/implement-models.md)
      - [Regression](advanced-statistics/implement-models/regression.md)
      - [Klassificering](advanced-statistics/implement-models/classification.md)
      - [Klustring](advanced-statistics/implement-models/clustering.md)
   - Exempel {#examples}
      - [Filtrera snabbt med statistik och maskininlärning](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [Förutse kundbortfall med SQL-baserad logistisk regression](advanced-statistics/examples/predict-customer-churn.md)
- Data Distiller-målgrupper {#data-distiller-audiences}
   - [Bygg externa målgrupper med SQL](data-distiller-audiences/overview.md)
- Exempel {#use-cases}
   - [Översikt](use-cases/overview.md)
   - [Bläddra överges](use-cases/abandoned-browse.md)
   - [Attributanalys](use-cases/attribution-analysis.md)
   - [Punktfiltrering](use-cases/bot-filtering.md)
   - [Rotfiltrering med statistik och introduktion av maskininlärning](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [Skapa en trendrapport över händelser](use-cases/trended-report-of-events.md)
   - [Samtyckesanalys](use-cases/consent-analysis.md)
   - [Kundens livstidsvärde](use-cases/customer-lifetime-value.md)
   - [Utforska data](./use-cases/data-exploration.md)
   - [Decile-baserade härledda datauppsättningar](use-cases/deciles-use-case.md)
   - [Fuzzy-matchning](use-cases/fuzzy-match.md)
   - [Visa en användares sidvyer](use-cases/list-visitor-sessions.md)
   - [Visa besökarna i deras sidvy](use-cases/visitors-by-number-of-page-views.md)
   - [Förutse kundbortfall med SQL](use-cases/predict-customer-churn-stub.md)
   - [Propensionstest](use-cases/propensity-score.md)
   - [Hämta liknande poster med funktioner i högre ordning](use-cases/retrieve-similar-records.md)
   - [Returnera och använda försäljningsvariabler från analysdata](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Visa sammanslagningsrapporten för en besökare](use-cases/roll-up-report-of-a-visitor.md)
   - [Insikter om webb- och mobilanalys](use-cases/analytics-insights.md)
- Viktiga begrepp {#key-concepts}
   - [Arbeta med kapslade datastrukturer](key-concepts/nested-data-structures.md)
   - [Förenkla kapslade datastrukturer](key-concepts/flatten-nested-data.md)
   - [Anonymt block](key-concepts/anonymous-block.md)
   - [Textbunden mall](key-concepts/inline-templates.md)
   - [Inkrementell inläsning](key-concepts/incremental-load.md)
   - [Datadeduplicering](key-concepts/deduplication.md)
   - [Datauppsättningsexempel](key-concepts/dataset-samples.md)
   - [Datauppsättningsstatistikberäkning](key-concepts/dataset-statistics.md)
- Data Distiller Hypercubes {#hypercubes}
   - [Effektiv big data-analys med hyperkuber](hypercubes/overview.md)
- Anslut klienter till frågetjänsten {#clients}
   - [Översikt över klientanslutningar](clients/overview.md)
   - [SSL-läge](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Användargränssnitt för frågetjänst {#ui}
   - [Översikt över användargränssnittet](ui/overview.md)
   - [Användarhandbok för Frågeredigeraren](ui/user-guide.md)
   - [Frågemallar](ui/query-templates.md)
   - [Parametriserade frågor](ui/parameterized-queries.md)
   - [Frågescheman](ui/query-schedules.md)
   - [Frågeloggar](ui/query-logs.md)
   - [Övervaka schemalagda frågor](ui/monitor-queries.md)
   - [Handbok för autentiseringsuppgifter](ui/credentials.md)
   - [Migrera JWT till OAuth-autentiseringsuppgifter](ui/migrate-jwt-to-oauth.md)
   - [Generera utdata från frågeresultat](ui/create-datasets.md)
- API för frågetjänst {#api}
   - [Komma igång](api/getting-started.md)
   - [Frågor](api/queries.md)
   - [Anslutningsparametrar](api/connection-parameters.md)
   - [Scheman](api/scheduled-queries.md)
   - [Körs för schemalagda frågor](api/runs-scheduled-queries.md)
   - [Frågemallar](api/query-templates.md)
   - [Snabbare frågor](api/accelerated-queries.md)
   - [Aviseringsprenumerationer](api/alert-subscriptions.md)
- Data Distiller Authorization API {#auth-api}
   - [Översikt](auth-api/overview.md)
   - [Komma igång](auth-api/getting-started.md)
   - [IP-åtkomst](auth-api/ip-access.md)
   - [Validera](auth-api/validate.md)
- Dataförvaltning {#data-governance}
   - [Översikt](data-governance/overview.md)
   - [Granskningsloggguide](data-governance/audit-log-guide.md)
   - [Identiteter i ad hoc-schemadatauppsättningar](data-governance/ad-hoc-schema-identities.md)
   - [Attributbaserad åtkomstkontroll för ad hoc-scheman](./data-governance/ad-hoc-schema-labels.md)
- Bästa praxis {#best-practices}
   - [Frågekörning](best-practices/writing-queries.md)
   - [Dataresursorganisation](./best-practices/organize-data-assets.md)
- SQL-referens {#sql}
   - [SQL-översikt](sql/overview.md)
   - [SQL-syntax](sql/syntax.md)
   - [Adobe-definierade funktioner](sql/adobe-defined-functions.md)
   - [Funktioner för högre ordning](sql/higher-order-functions.md)
   - [Spark SQL-funktioner](sql/spark-sql-functions.md)
   - [Metadata-kommandon](sql/metadata.md)
   - [Förberedda programsatser](sql/prepared-statements.md)
- [Vanliga frågor och svar](troubleshooting-guide.md)
- [IP-adress tillåtelselista](ip-address-allowlist.md)
- [API-referens](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Versionsinformation om Experience Platform](https://experienceleague.adobe.com/sv/docs/experience-platform/release-notes/latest)
