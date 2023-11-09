---
audience: user
user-guide-title: Hjälp med Adobe Experience Platform Query Service
breadcrumb-title: Användarhandbok om Query Service
user-guide-description: Använd standard-SQL för att fråga efter data i datasjön i Experience Platform.
feature: Queries
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 12%

---


# Adobe Experience Platform Query Service {#query}

- [Översikt över frågetjänsten](home.md)
- [Paket för frågetjänst](packaging.md)
- [Skyddsutkast för frågetjänst](guardrails.md)
- Kom igång {#get-started}
   - [Förutsättningar](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Översikt](data-distiller/overview.md)
   - [Licensanvändning](data-distiller/license-usage.md)
   - Query Accelerated Store {#query-accelerated-store}
      - [Skicka accelererade frågor](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Datamodellguide för rapportinsikter](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Härledda attribut {#derived-attributes}
      - [Översikt](data-distiller/derived-attributes/overview.md)
      - [Sömlöst SQL-flöde](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Skapa decimalbaserade härledda attribut](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - AI/ML-rörledningar {#ml-feature-pipelines}
      - [Översikt](data-distiller/ml-feature-pipelines/overview.md)
      - [Anslut till Jupyter-anteckningsböcker](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Förberedande dataanalys](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Teknikfunktioner för XML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportera data till ML-miljöer](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML-arbetsflöde för berikning av data från början till slut](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Användningsfall {#use-cases}
   - [Bläddra överges](use-cases/abandoned-browse.md)
   - [Attributanalys](use-cases/attribution-analysis.md)
   - [Punktfiltrering](use-cases/bot-filtering.md)
   - [Skapa en trendrapport över händelser](use-cases/trended-report-of-events.md)
   - [Samtyckesanalys](use-cases/consent-analysis.md)
   - [Kundens livstidsvärde](use-cases/customer-lifetime-value.md)
   - [Lövbaserade härledda attribut](use-cases/deciles-use-case.md)
   - [Fuzzy-matchning](use-cases/fuzzy-match.md)
   - [Visa en användares sidvyer](use-cases/list-visitor-sessions.md)
   - [Visa besökarna i deras sidvy](use-cases/visitors-by-number-of-page-views.md)
   - [Propensionstest](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Returnera och använda försäljningsvariabler från analysdata](use-cases/merchandising-variables.md)
   - [Visa sammanslagningsrapporten för en besökare](use-cases/roll-up-report-of-a-visitor.md)
   - [Insikter om webb- och mobilanalys](use-cases/analytics-insights.md)
- Anslut klienter till frågetjänsten {#clients}
   - [Översikt över klientanslutningar](clients/overview.md)
   - [SSL-läge](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
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
   - [Generera utdata från frågeresultat](ui/create-datasets.md)
- API-slutpunkter för frågetjänst {#api}
   - [Komma igång](api/getting-started.md)
   - [Frågor](api/queries.md)
   - [Anslutningsparametrar](api/connection-parameters.md)
   - [Scheman](api/scheduled-queries.md)
   - [Körs för schemalagda frågor](api/runs-scheduled-queries.md)
   - [Frågemallar](api/query-templates.md)
   - [Snabbare frågor](api/accelerated-queries.md)
   - [Aviseringsprenumerationer](api/alert-subscriptions.md)
- Datastyrning {#data-governance}
   - [Översikt](data-governance/overview.md)
   - [Granskningsloggguide](data-governance/audit-log-guide.md)
   - [Identiteter i ad hoc-schemadatauppsättningar](data-governance/ad-hoc-schema-identities.md)
   - [Attributbaserad åtkomstkontroll för ad hoc-scheman](./data-governance/ad-hoc-schema-labels.md)
- God praxis {#best-practices}
   - [Frågekörning](best-practices/writing-queries.md)
   - [Dataresursorganisation](./best-practices/organize-data-assets.md)
- Grundläggande begrepp {#essential-concepts}
   - [Arbeta med kapslade datastrukturer](essential-concepts/nested-data-structures.md)
   - [Förenkla kapslade datastrukturer](essential-concepts/flatten-nested-data.md)
   - [Anonymt block](essential-concepts/anonymous-block.md)
   - [Textbunden mall](essential-concepts/inline-templates.md)
   - [Inkrementell inläsning](essential-concepts/incremental-load.md)
   - [Datadeduplicering](essential-concepts/deduplication.md)
   - [Datauppsättningsexempel](essential-concepts/dataset-samples.md)
   - [Datauppsättningsstatistikberäkning](essential-concepts/dataset-statistics.md)
- SQL-referens {#sql}
   - [SQL-översikt](sql/overview.md)
   - [SQL-syntax](sql/syntax.md)
   - [Funktioner som definieras av Adobe](sql/adobe-defined-functions.md)
   - [Spark SQL-funktioner](sql/spark-sql-functions.md)
   - [Metadata-kommandon](sql/metadata.md)
   - [Förberedda programsatser](sql/prepared-statements.md)
- [Frågor och svar](troubleshooting-guide.md)
- [IP-adress tillåtelselista](ip-address-allowlist.md)
- [API-referens](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)
