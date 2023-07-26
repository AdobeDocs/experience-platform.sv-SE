---
keywords: Experience Platform;hem;populära ämnen;källkopplingar;källanslutning;källor;datakällor;datakällor;datakällanslutning;datakällanslutning
solution: Experience Platform
title: Översikt över källkopplingar
description: Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: a848ea11e388678ade780fd81ef3ff6a3477b741
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserade lager, databaser och många andra.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom plattformen. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program {#adobe-applications}

Experience Platform tillåter att data kan hämtas från andra Adobe-program, inklusive Adobe Analytics och Adobe Audience Manager. Mer information finns i följande relaterade dokument:

- [Översikt över Adobe Audience Manager-källa](connectors/adobe-applications/audience-manager.md)
   - [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Översikt över datakällan för Adobe Analytics Classics](connectors/adobe-applications/classifications.md)
   - [Skapa en Adobe Analytics Classifications-datakällanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/classifications.md)
- [Översikt över datakällan i Adobe Analytics Report Suite](connectors/adobe-applications/analytics.md)
   - [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Översikt över Adobe Campaign Managed Cloud Services-källa](connectors/adobe-applications/campaign.md)
   - [Skapa en Adobe Campaign Managed Cloud Services-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/campaign.md)
- [Översikt över Adobe Commerce-källa](connectors/adobe-applications/commerce.md)
- [Översikt över datakällan för Adobe Data Collection](connectors/adobe-applications/data-collection.md)
   - [Skapa en källanslutning för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] källöversikt](connectors/adobe-applications/marketo/marketo.md)
   - [Skapa en [!DNL Marketo Engage] källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Skapa en [!DNL Marketo Engage] källanslutning och dataflöde för anpassade aktivitetsdata](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Översikt över Adobe Workfront-källa](connectors/adobe-applications/workfront.md)
   - [Skapa en Workfront-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Google Ads](connectors/advertising/ads.md)

### Analytics  {#analytics}

Experience Platform stöder inmatning av data från en analysplattform från tredje part. Mer information finns i följande relaterade dokument:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md)
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md)

### molnlagring {#cloud-storage}

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Samtycke och inställningar {#consent}

Experience Platform har stöd för inmatning av data från en plattform för hantering av samtycke och preferenser från tredje part. Mer information finns i följande relaterade dokument:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### Kundrelationshantering (CRM) {#customer-relationship-management}

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce]. Mer information finns i följande relaterade dokument:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Nöjda kunder {#customer-success}

Experience Platform har stöd för inhämtning av data från tredjepartsprogram. Mer information finns i följande relaterade dokument:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### Databas {#database}

Experience Platform har stöd för att importera data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake (Streaming)]](connectors/databases//snowflake-streaming.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### eCommerce {#ecommerce}

Experience Platform stöder inmatning av data från ett e-handelssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md)
- [[!DNL Shopify]](connectors/ecommerce/shopify.md)
- [[!DNL Shopify (Streaming)]](connectors/ecommerce/shopify-streaming.md)

### Lokalt system {#local-system}

Experience Platform har stöd för inmatning av data från ditt lokala system. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Lokal filöverföring](connectors/local-system/local-file-upload.md)

### Marknadsföringsautomatisering {#marketing-automation}

Experience Platform stöder inmatning av data från ett system för automatisering av marknadsföring från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Betalningar {#payments}

Experience Platform stöder inmatning av data från tredje parts betalningssystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Direktuppspelning {#streaming}

Experience Platform stöder inmatning av data från strömningskällor. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protokoll {#protocols}

Experience Platform har stöd för inmatning av data från ett tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras inom Adobe Admin Console. Du kan komma åt behörigheter via **[!UICONTROL Permissions]** i en viss produktprofil. Från **[!UICONTROL Edit Permissions]** kan du komma åt källbehörigheterna via **[!UICONTROL data ingestion]** menyalternativ. The **[!UICONTROL View Sources]** behörighet ger skrivskyddad åtkomst till tillgängliga källor i **[!UICONTROL Catalog]** och autentiserade källor i **[!UICONTROL Browse]** -tabb, medan **[!UICONTROL Manage Sources]** ger fullständig åtkomst för att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL View Sources]** På | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken Katalog samt på flikarna Bläddra, Konton och Dataflöde. |
| **[!UICONTROL Manage Sources]** På | Förutom funktionerna i **[!UICONTROL View Sources]**, ger åtkomst till **[!UICONTROL Connect Source]** alternativ i **[!UICONTROL Catalog]** och till **[!UICONTROL Select Data]** alternativ i **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** kan du även aktivera eller inaktivera **[!UICONTROL DataFlows]** och redigera sina scheman. |
| **[!UICONTROL View Sources]** Av och **[!UICONTROL Manage Sources]** Av | Återkalla all åtkomst till källor. |

Mer information om vilka behörigheter som ges via behörigheter i Adobe finns i [åtkomstkontroll - översikt](../access-control/home.md).

### Attributbaserad åtkomstkontroll

Med attributbaserad åtkomstkontroll i Adobe Experience Platform kan administratörer styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut.

Med attributbaserad åtkomstkontroll kan du tillämpa mappningskonfigurationer på fält som du har behörighet till. Dessutom kan du inte importera data till en datauppsättning om du inte har tillgång till alla fält i datauppsättningen.

#### Stöd för attributbaserad åtkomstkontroll i källor

>[!TIP]
>
>Attributbaserad åtkomstkontroll fungerar så här: **roller** skapas för att kategorisera de typer av användare som interagerar med din plattformsinstans. **Etiketter** används på **roller** för att utse åtkomsten till den angivna rollen. **Etiketter** används även för resurser som schemafält och segment. För att en användare ska ha tillgång till vissa schemafält och segment måste de läggas till i *en roll med samma etikett som tilldelas den efterfrågade resursen*. Mer information finns i [attribueringsbaserad åtkomstkontroll från början till slut](../access-control/abac/end-to-end-guide.md).

- Använd etiketter på schemafält för att definiera åtkomst till specifika schemafält i organisationen. När åtkomsten till specifika schemafält har upprättats kan användare bara skapa mappningar för de fält som de har åtkomst till.
- Användare utan rätt roller kan inte skapa eller uppdatera dataflöden med mappningar som innehåller otillgängliga schemafält. Dessutom kan obehöriga användare inte uppdatera, ta bort, aktivera eller inaktivera befintliga dataflöden med otillgängliga schemafält.
- Dessutom måste ett dataflöde ha exakt samma schema-ID och version i mappningen, måldatauppsättningen och målanslutningen.

Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll - översikt](../access-control/abac/overview.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som beta (&quot;Beta&quot;) bekräftar du härmed att betaversionen tillhandahålls ***&quot;i befintligt skick&quot; utan någon garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, ändra eller på annat sätt stödja betaversionen. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att betaversionen och/eller det medföljande materialet fungerar som de ska. Beta betraktas som konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om betaversionen, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder betaversionen, förslag, förbättringar och rekommendationer) som du ger dig till Adobe tilldelas Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
