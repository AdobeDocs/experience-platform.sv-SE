---
audience: user
user-guide-title: Hjälp om Adobe Experience Platform Query Service
breadcrumb-title: Handbok för frågetjänst
user-guide-description: Använd standard-SQL för att fråga efter data i datasjön i Experience Platform.
feature: Queries
source-git-commit: bbe67d03834f3da0e781bc0f86024870db612cfe
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 5%

---


# Adobe Experience Platform Query Service {#query}

- [Översikt över frågetjänsten](home.md)
- [Paket för frågetjänst](packages.md)
- [Skyddsutkast för frågetjänst](guardrails.md)
- Data Distiller {#data-distiller}
   - [Licensanvändning](data-distiller/licence-usage.md)
- Kom igång {#get-started}
   - [Förutsättningar](get-started/prerequisites.md)
- Användningsfall {#use-cases}
   - [Övergiven surfning](use-cases/abandoned-browse.md)
   - [Aktivitetsanalys med Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Attributanalys](use-cases/attribution-analysis.md)
   - [Punktfiltrering](use-cases/bot-filtering.md)
   - [Insikter om webb- och mobilanalys](use-cases/analytics-insights.md)
- API för frågetjänst {#api}
   - [Komma igång](api/getting-started.md)
   - [Frågor](api/queries.md)
   - [Anslutningsparametrar](api/connection-parameters.md)
   - [Schemalagda frågor](api/scheduled-queries.md)
   - [Körs för schemalagda frågor](api/runs-scheduled-queries.md)
   - [Frågemallar](api/query-templates.md)
- Användargränssnitt för frågetjänst {#ui}
   - [Översikt över användargränssnittet](ui/overview.md)
   - [Användarhandbok för Frågeredigeraren](ui/user-guide.md)
   - [Frågemallar](ui/query-templates.md)
   - [Använda autentiseringsuppgifter för frågetjänsten](ui/credentials.md)
   - [Genererar datauppsättningar från frågeresultat](ui/create-datasets.md)
- [Query Accelerated Store]{#query-accelerated-store}
   - [Datamodell för rapportinsikter](query-accelerated-store/reporting-insights-data-model.md)
- God praxis {#best-practices}
   - [Allmän vägledning för frågekörning](best-practices/writing-queries.md)
   - [Vägledning för organisationen av datatillgångar](./best-practices/organize-data-assets.md)
   - [Arbeta med kapslade datastrukturer](best-practices/nested-data-structures.md)
   - [Förenkla kapslade datastrukturer](best-practices/flatten-nested-data.md)
   - [Anonymt block](best-practices/anonymous-block.md)
   - [Inkrementell inläsning](best-practices/incremental-load.md)
   - [Datadeduplicering](best-practices/deduplication.md)
- Härledda attribut {#derived-attributes}
   - [Översikt](derived-attributes/overview.md)
   - [Användningsfall för decimaler](derived-attributes/deciles-use-case.md)
- Exempelfrågor {#sample-queries}
   - [Exempelfrågor om Experience Event](sample-queries/experience-event.md)
   - [Exempel på Adobe Analytics-frågor](sample-queries/adobe-analytics.md)
- SQL-referens {#sql}
   - [SQL-översikt](sql/overview.md)
   - [SQL-syntax](sql/syntax.md)
   - [Adobe-definierade funktioner](sql/adobe-defined-functions.md)
   - [Spark SQL-funktioner](sql/spark-sql-functions.md)
   - [Metadata-kommandon](sql/metadata.md)
   - [Förberedda programsatser](sql/prepared-statements.md)
   - [Datauppsättningsexempel](sql/dataset-samples.md)
- Anslut klienter till frågetjänsten {#clients}
   - [Översikt över klientanslutningar](clients/overview.md)
   - [SSL-lägen](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [Databasvisualisering](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Datastyrning {#data-governance}
   - [Översikt](data-governance/overview.md)
   - [Granskningsloggguide](data-governance/audit-log-guide.md)
   - [Identiteter i ad hoc-schemadatauppsättningar](data-governance/ad-hoc-schema-identities.md)
   - [Attributbaserad åtkomstkontroll för ad hoc-scheman](./data-governance/ad-hoc-schema-labels.md)
- [Felsökningsguide](troubleshooting-guide.md)
- [API-referens](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Versionsinformation för plattform](https://www.adobe.com/go/platform-release-notes-en)