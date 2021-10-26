---
keywords: Experience Platform;hem;populära ämnen;källkopplingar;källanslutning;källor;datakällor;datakällor;datakällanslutning;datakällanslutning
solution: Experience Platform
title: Översikt över källkopplingar
topic-legacy: overview
description: Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: f8cecdaaab3d98c7f6542b51dc764a019b04b0b1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserade lager, databaser och många andra.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom plattformen. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program

Experience Platform tillåter att data hämtas från andra Adobe-program, inklusive Adobe Analytics och Adobe Audience Manager. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager Connector - översikt](connectors/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Översikt över anslutningen till datakällan i Adobe Analytics Classics](connectors/adobe-applications/classifications.md)
- [Skapa en Adobe Analytics Classifications-datakällanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics Report Suite - anslutningsöversikt för datakälla](connectors/adobe-applications/analytics.md)
- [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Skapa en källanslutning för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] anslutningsöversikt](connectors/adobe-applications/marketo/marketo.md)
- [Skapa en [!DNL Marketo Engage] källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/marketo.md)

### Reklam

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) koppling

### molnlagring

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

- [[!DNL Azure Data Lake Storage Gen2] koppling](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] koppling](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] koppling](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] koppling](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] koppling](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] koppling](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] koppling](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP] koppling](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] koppling](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] koppling](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] koppling](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] koppling](connectors/cloud-storage/sftp.md)

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce]. Mer information finns i följande relaterade dokument:

- [[!DNL Microsoft Dynamics] koppling](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] koppling](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Nöjda kunder

Experience Platform har stöd för inhämtning av data från tredjepartsprogram. Mer information finns i följande relaterade dokument:

- [[!DNL Salesforce Service Cloud] koppling](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] koppling](connectors/customer-success/servicenow.md)

### Databas

Experience Platform har stöd för att importera data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Amazon Redshift] koppling](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] koppling](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] koppling](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] koppling](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] koppling](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] koppling](connectors/databases/ats.md)
- [[!DNL Couchbase] koppling](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] koppling](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] koppling](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] koppling](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] koppling](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] koppling](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] koppling](connectors/databases/sql-server.md)
- [[!DNL MySQL] koppling](connectors/databases/mysql.md)
- [[!DNL Oracle] koppling](connectors/databases/oracle.md)
- [[!DNL Phoenix] koppling](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] koppling](connectors/databases/postgres.md)
- [[!DNL Snowflake] koppling](connectors/databases/snowflake.md)

### eCommerce

Experience Platform stöder inmatning av data från ett e-handelssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokalt system

Experience Platform har stöd för inmatning av data från ditt lokala system. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Lokal filöverföring](connectors/local-system/local-file-upload.md)

### Marknadsföringsautomatisering

Experience Platform stöder inmatning av data från ett system för automatisering av tredjepartsmarknadsföring. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL HubSpot] koppling](connectors/marketing-automation/hubspot.md)
- [[!DNL MailChimp Campaign]](./tutorials/api/create/marketing-automation/mailchimp-campaign.md)
- [[!DNL MailChimp Members]](./tutorials/api/create/marketing-automation/mailchimp-members.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Betalningar

Experience Platform stöder inmatning av data från tredje parts betalningssystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL PayPal] koppling](connectors/payments/paypal.md)

### Direktuppspelning

Experience Platform stöder inmatning av data från strömningskällor. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protokoll

Experience Platform har stöd för inmatning av data från tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Generic OData] koppling](connectors/protocols/odata.md)

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras inom Adobe Admin Console. Du kan komma åt behörigheter via **[!UICONTROL Permissions]** i en viss produktprofil. Från **[!UICONTROL Edit Permissions]** kan du komma åt källbehörigheterna via **[!UICONTROL data ingestion]** menyalternativ. The **[!UICONTROL View Sources]** behörighet ger skrivskyddad åtkomst till tillgängliga källor i **[!UICONTROL Catalog]** och autentiserade källor i **[!UICONTROL Browse]** -tabb, medan **[!UICONTROL Manage Sources]** ger fullständig åtkomst för att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL View Sources]** På | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken Katalog samt på flikarna Bläddra, Konton och Dataflöde. |
| **[!UICONTROL Manage Sources]** På | Förutom funktionerna i **[!UICONTROL View Sources]**, ger åtkomst till **[!UICONTROL Connect Source]** alternativ i **[!UICONTROL Catalog]** och till **[!UICONTROL Select Data]** alternativ i **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** kan du även aktivera eller inaktivera **[!UICONTROL DataFlows]** och redigera sina scheman. |
| **[!UICONTROL View Sources]** Av och **[!UICONTROL Manage Sources]** Av | Återkalla all åtkomst till källor. |

Mer information om de behörigheter som beviljas via Admin Console, inklusive dessa fyra källor, finns i [åtkomstkontroll - översikt](../access-control/home.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som beta (&quot;Beta&quot;) bekräftar du härmed att betaversionen tillhandahålls ***&quot;i befintligt skick&quot; utan någon garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, ändra eller på annat sätt stödja betaversionen. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att betaversionen och/eller det medföljande materialet fungerar som de ska. Beta betraktas som konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om betaversionen, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder betaversionen, förslag, förbättringar och rekommendationer) som du ger dig till Adobe tilldelas Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
