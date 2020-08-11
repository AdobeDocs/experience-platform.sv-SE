---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Source Connectors - översikt
topic: overview
translation-type: tm+mt
source-git-commit: 8e39cc206efa3fc314ae689845c88f0923ac1743
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---


# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med [!DNL Experience Platform]hjälp av kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

## Typer av källor

Källor i [!DNL Experience Platform] är grupperade i följande kategorier:

### Adobe-program

[!DNL Experience Platform] tillåter att data hämtas från andra Adobe-program, inklusive Adobe Analytics, Adobe Audience Manager och [!DNL Experience Platform Launch]. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager Connector - översikt](connectors/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics dataanslutning - översikt](connectors/adobe-applications/analytics.md)
- [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Skapa en källkoppling för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reklam

[!DNL Experience Platform] ger stöd för inmatning av data från ett annonssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [!DNL Google AdWords](connectors/advertising/ads.md) koppling

### molnlagring

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) koppling
- [!DNL Azure Blob](connectors/cloud-storage/blob.md) koppling
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) koppling
- [!DNL Amazon S3](connectors/cloud-storage/s3.md) koppling
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) koppling
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) koppling
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) koppling
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) koppling
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) koppling

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. [!DNL Experience Platform] har stöd för att importera CRM-data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce]. Mer information finns i följande relaterade dokument:

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) koppling
- [!DNL Salesforce](connectors/crm/salesforce.md) koppling

### Nöjda kunder

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsapp för kundframgångar. Mer information finns i följande relaterade dokument:

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) koppling
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) koppling

### Databas

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [!DNL Amazon Redshift](connectors/databases/redshift.md) koppling
- [!DNL Apache Hive on Azure HDInsights](connectors/databases/hive.md) koppling
- [!DNL Apache Spark on Azure HDInsights](connectors/databases/spark.md) koppling
- [!DNL Azure Data Explorer](connectors/databases/data-explorer.md) koppling
- [!DNL Azure Synapse Analytics](connectors/databases/synapse-analytics.md) koppling
- [!DNL Azure Table Storage](connectors/databases/ats.md) koppling
- [!DNL Couchbase](connectors/databases/couchbase.md) koppling
- [!DNL Google BigQuery](connectors/databases/bigquery.md) koppling
- [!DNL GreenPlum](connectors/databases/greenplum.md) koppling
- [!DNL HP Vertica](connectors/databases/hp-vertica.md) koppling
- [!DNL IBM DB2](connectors/databases/ibm-db2.md) koppling
- [!DNL MariaDB](connectors/databases/mariadb.md) koppling
- [!DNL Microsoft SQL Server](connectors/databases/sql-server.md) koppling
- [!DNL MySQL](connectors/databases/mysql.md) koppling
- [!DNL Oracle](connectors/databases/oracle.md) koppling
- [!DNL Phoenix](connectors/databases/phoenix.md) koppling
- [!DNL PostgreSQL](connectors/databases/postgres.md) koppling

### Marknadsföringsautomatisering

[!DNL Experience Platform] har stöd för inmatning av data från ett automatiseringssystem för marknadsföring från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) koppling

### Betalningar

[!DNL Experience Platform] har stöd för inmatning av data från ett betalningssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [!DNL PayPal](connectors/payments/paypal.md) koppling

### Protokoll

[!DNL Experience Platform] har stöd för inmatning av data från ett tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [!DNL Generic OData](connectors/protocols/odata.md) koppling

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras inom Adobe Admin Console. Du kan få åtkomst till behörigheter via fliken *[!UICONTROL Permissions]* i en viss produktprofil. Från **[!UICONTROL Edit Permissions]** panelen kan du komma åt de behörigheter som gäller för källor via *[!UICONTROL data ingestion]* menyalternativet. Behörigheten **[!UICONTROL View Sources]** ger skrivskyddad åtkomst till tillgängliga källor på *[!UICONTROL Catalog]* fliken och till autentiserade källor på *[!UICONTROL Browse]* **[!UICONTROL Manage Sources]** fliken, medan behörigheten ger fullständig åtkomst för att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL View Sources]** På | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken *Katalog* , samt flikarna *Bläddra*, *Konton* och *DataFlow* . |
| **[!UICONTROL Manage Sources]** På | Förutom de funktioner som ingår i **[!UICONTROL View Sources]** ger tillgång till *[!UICONTROL Connect Source]* alternativen i *[!UICONTROL Catalog]* och till *[!UICONTROL Select Data]* alternativen i *[!UICONTROL Browse]*. **[!UICONTROL Manage Sources]** kan du även aktivera eller inaktivera *[!UICONTROL DataFlows]* och redigera deras scheman. |
| **[!UICONTROL View Sources]** Av och **[!UICONTROL Manage Sources]** Av | Återkalla all åtkomst till källor. |

Mer information om de behörigheter som ges via Admin Console, inklusive dessa fyra källor, finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som beta (&quot;Beta&quot;) bekräftar du härmed att betaversionen tillhandahålls ***&quot;som den är&quot; utan någon garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, ändra eller på annat sätt stödja betaversionen. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att betaversionen och/eller det medföljande materialet fungerar som de ska. Beta betraktas som konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om betaversionen, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder betaversionen, förslag, förbättringar och rekommendationer) som du ger dig till Adobe tilldelas Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
