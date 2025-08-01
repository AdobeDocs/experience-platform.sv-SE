---
keywords: Experience Platform;hem;populära ämnen;källanslutningar;källanslutning;källor;datakällor;datakälla;datakällanslutning
solution: Experience Platform
title: Source Connectors Overview
description: Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 7596a87309105897a2727faa8e22b06cdf5547c3
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 0%

---

# Source Connectors overview

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserade lager, databaser och många andra.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom Experience Platform. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Adobe-byggda och partnerbyggda källor {#adobe-and-partner-built-sources}

Vissa av anslutningarna i Experience Platform-källkatalogen byggs och underhålls av Adobe, medan andra byggs och underhålls av partnerföretag med hjälp av [Källorna i SDK](/help/sources/sources-sdk/overview.md). En anteckning högst upp på dokumentationssidan för varje partnerbyggd koppling anropar om en källa skapas och underhålls av partnern. Till exempel skapas [Amazon S3-kopplingen](/help/sources/connectors/cloud-storage/s3.md) av Adobe medan [RainFocus-kopplingen](/help/sources/connectors/analytics/rainfocus.md) skapas och underhålls av RainFocus-teamet.

För partnerskapade och underhållna anslutningar innebär detta att problem med kopplingen kan behöva lösas av partnerteamet (kontaktmetoden finns i anteckningen på dokumentationssidan). Kontakta Adobe eller kundtjänst om du har problem med kontakter som skapats och underhålls av Adobe.

>[!ENDSHADEBOX]

## Källkatalog

I följande avsnitt finns en lista med alla tillgängliga källor i källkatalogen.

### Adobe-program {#adobe-applications}

Med Experience Platform kan data hämtas från andra Adobe-program, inklusive Adobe Analytics och Adobe Audience Manager. Läs följande relaterade dokument för mer information:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics-klassificeringsdata](connectors/adobe-applications/classifications.md)
   - [Skapa en Adobe Analytics Classifications-datakällanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics Report Suite-data](connectors/adobe-applications/analytics.md)
   - [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Skapa en Adobe Campaign Managed Cloud Services-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Adobe Data Collection](connectors/adobe-applications/data-collection.md)
   - [Skapa en källanslutning för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Skapa en  [!DNL Marketo Engage] källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Skapa en  [!DNL Marketo Engage] källanslutning och ett dataflöde för anpassade aktivitetsdata](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Avancerade företagskällor {#advanced-enterprise-sources}

Följande källor är endast tillgängliga för [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/se/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)-kunder.

| Source | Kategori | Inmatningstyp | Cloud |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | molnlagring | Direktuppspelning | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Databas | Grupp | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Databas | Grupp | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | molnlagring | Direktuppspelning | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Databas | Grupp | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Databas | Grupp | Azure |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | molnlagring | Direktuppspelning | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Databas | Direktuppspelning | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Databas | Grupp | Azure, AWS |

{style="table-layout:auto"}

### Advertising {#advertising}

Du kan använda följande källor för att importera annonsdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [Google Ads](connectors/advertising/ads.md) | Grupp | Azure |

{style="table-layout:auto"}

### Analytics  {#analytics}

Du kan använda följande källor för att importera analysdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Grupp | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Direktuppspelning | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Direktuppspelning | Azure |

{style="table-layout:auto"}

### molnlagring {#cloud-storage}

Lagringskällor i molnet kan överföra dina egna data till Experience Platform utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

Du kan använda följande källor för att importera molnlagringsdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Grupp | Azure |
| [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) | Grupp | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Grupp | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Grupp | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Grupp | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Grupp | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Grupp | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Grupp | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Grupp | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Grupp | Azure |

{style="table-layout:auto"}

### Samtycke och inställningar {#consent}

Du kan använda följande källor för att importera data för samtycke och inställningar till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Direktuppspelning | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Grupp | Azure |

{style="table-layout:auto"}

### Kundrelationshantering (CRM) {#customer-relationship-management}

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för inhämtning av CRM-data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce]. Mer information finns i följande relaterade dokument:

Du kan använda följande källor för att importera CRM-data till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Grupp | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Grupp | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Grupp | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Grupp | Azure |

{style="table-layout:auto"}

### Nöjda kunder {#customer-success}

Du kan använda följande källor för att importera kunddata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Grupp | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Grupp | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Grupp | Azure |

{style="table-layout:auto"}

### Databas {#database}

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

Du kan använda följande källor för att importera data från din databas till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Grupp | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Grupp | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Grupp | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Grupp | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Grupp | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Grupp | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Grupp | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Grupp | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Grupp | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Grupp | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Grupp | Azure |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Grupp | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Grupp | Azure |

{style="table-layout:auto"}

### Data- och identitetspartners {#data-partner}

Du kan använda följande källor för att importera data och identitetspartnerdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Grupp | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Grupp | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Grupp | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Grupp | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Grupp | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Grupp | Azure |

{style="table-layout:auto"}

### e-handel {#ecommerce}

Du kan använda följande källor för att importera e-handelsdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Grupp | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Grupp | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Direktuppspelning | Azure |

{style="table-layout:auto"}

### Lokalt system {#local-system}

Du kan använda följande källor för att importera data från ditt lokala system till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [Lokal filöverföring](connectors/local-system/local-file-upload.md) | Grupp | Azure |

{style="table-layout:auto"}

### Marknadsföringsautomatisering {#marketing-automation}

Du kan använda följande källor för att importera automatiserade marknadsföringsdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Direktuppspelning | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Direktuppspelning | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Direktuppspelning | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Grupp | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Grupp | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Grupp | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Grupp | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Grupp | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Grupp | Azure, AWS |

{style="table-layout:auto"}

### Betalningar {#payments}

Du kan använda följande källor för att importera betalningsdata till Experience Platform.

| Source | Inmatningstyp | Cloud |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Grupp | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Grupp | Azure |

{style="table-layout:auto"}

### Direktuppspelning {#streaming}

Du kan använda följande källor för att strömma data till Experience Platform.

| Source | Inmatningstyp | Molnsupport |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Direktuppspelning | Azure, AWS |

{style="table-layout:auto"}

### Protokoll {#protocols}

Du kan använda följande källor för att importera protokolldata till Experience Platform.

| Source | Inmatningstyp | Molnsupport |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Grupp | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Grupp | Azure |

{style="table-layout:auto"}

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras inom Adobe Admin Console. Du kan få åtkomst till behörigheter via fliken **[!UICONTROL Permissions]** i en viss produktprofil. Från panelen **[!UICONTROL Edit Permissions]** kan du komma åt de behörigheter som gäller för källor via menyposten **[!UICONTROL data ingestion]**. **[!UICONTROL View Sources]**-behörigheten ger skrivskyddad åtkomst till tillgängliga källor på fliken **[!UICONTROL Catalog]** och autentiserade källor på fliken **[!UICONTROL Browse]**, medan behörigheten **[!UICONTROL Manage Sources]** ger fullständig åtkomst för att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL View Sources]** på | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken Katalog samt på flikarna Bläddra, Konton och Dataflöde. |
| **[!UICONTROL Manage Sources]** på | Förutom funktionerna i **[!UICONTROL View Sources]** ger åtkomst till alternativet **[!UICONTROL Connect Source]** i **[!UICONTROL Catalog]** och till alternativet **[!UICONTROL Select Data]** i **[!UICONTROL Browse]**. Med **[!UICONTROL Manage Sources]** kan du även aktivera eller inaktivera **[!UICONTROL DataFlows]** och redigera deras scheman. |
| **[!UICONTROL View Sources]** av och **[!UICONTROL Manage Sources]** av | Återkalla all åtkomst till källor. |

Mer information om de behörigheter som ges via Adobe-behörigheter finns i [åtkomstkontrollsöversikten](../access-control/home.md).

### Attributbaserad åtkomstkontroll

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Med attributbaserad åtkomstkontroll kan du tillämpa mappningskonfigurationer på fält som du har behörighet till. Dessutom kan du inte importera data till en datauppsättning om du inte har tillgång till alla fält i datauppsättningen.

#### Stöd för attributbaserad åtkomstkontroll i källor

>[!TIP]
>
>Attributbaserad åtkomstkontroll fungerar så här: **roller** skapas för att kategorisera de typer av användare som interagerar med din Experience Platform-instans. **Etiketter** används på **roller** för att ange åtkomst för den angivna rollen. **Etiketter** används också för resurser som schemafält och segment. För att en användare ska ha åtkomst till vissa schemafält och segment måste de läggas till i *en roll med samma etikett som tilldelats den efterfrågade resursen*. Mer information finns i [attributbaserad åtkomstkontroll från början till slut](../access-control/abac/end-to-end-guide.md).

- Använd etiketter på schemafält för att definiera åtkomst till specifika schemafält i organisationen. När åtkomsten till specifika schemafält har upprättats kan användare bara skapa mappningar för de fält som de har åtkomst till.
- Användare utan rätt roller kan inte skapa eller uppdatera dataflöden med mappningar som innehåller otillgängliga schemafält. Dessutom kan obehöriga användare inte uppdatera, ta bort, aktivera eller inaktivera befintliga dataflöden med otillgängliga schemafält.
- Dessutom måste ett dataflöde ha exakt samma schema-ID och version i mappningen, måldatauppsättningen och målanslutningen.

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontrollsöversikt](../access-control/abac/overview.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som betaversion (&quot;Beta&quot;) bekräftar du härmed att Beta tillhandahålls ***i befintligt skick utan garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt stödja Beta. Du rekommenderas att använda Informativ och inte på något sätt förlita dig på att sådana Beta och/eller medföljande material fungerar korrekt eller fungerar korrekt. Beta betraktas som Konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om Beta, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder Beta, förslag, förbättringar och rekommendationer) som du ger Adobe tilldelas härmed till Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
