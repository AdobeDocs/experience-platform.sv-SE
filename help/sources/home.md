---
keywords: Experience Platform;hem;populära ämnen;källkopplingar;källanslutning;källor;datakällor;datakällor;datakällanslutning;datakällanslutning
solution: Experience Platform
title: Översikt över källkopplingar
topic: översikt
description: Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.
translation-type: tm+mt
source-git-commit: b8f7f6e7f110dc9ebd025cd594fd1a54126ccdf3
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---


# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserade lager, databaser och många andra.

[!DNL Flow Service] används för att samla in och centralisera kunddata från olika källor inom plattformen. Tjänsten tillhandahåller ett användargränssnitt och RESTful API som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program

Experience Platform tillåter att data hämtas från andra Adobe-program, inklusive Adobe Analytics, Adobe Audience Manager och [!DNL Experience Platform Launch]. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager Connector - översikt](connectors/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics Classifications Data Connector - översikt](connectors/adobe-applications/classifications.md)
- [Skapa en Adobe Analytics Classifications-datakällanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics dataanslutning - översikt](connectors/adobe-applications/analytics.md)
- [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Skapa en källanslutning för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)

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
- [[!DNL FTP] koppling](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] koppling](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] koppling](connectors/cloud-storage/google-pubsub.md)
- [[!DNL SFTP] koppling](connectors/cloud-storage/sftp.md)

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från [!DNL Microsoft Dynamics 365] och [!DNL Salesforce]. Mer information finns i följande relaterade dokument:

- [[!DNL Microsoft Dynamics] koppling](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] koppling](connectors/crm/salesforce.md)

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
- [[!DNL Microsoft SQL Server] koppling](connectors/databases/sql-server.md)
- [[!DNL MySQL] koppling](connectors/databases/mysql.md)
- [[!DNL Oracle] koppling](connectors/databases/oracle.md)
- [[!DNL Phoenix] koppling](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] koppling](connectors/databases/postgres.md)

### eCommerce

Experience Platform stöder inmatning av data från ett e-handelssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Marknadsföringsautomatisering

Experience Platform stöder inmatning av data från ett system för automatisering av tredjepartsmarknadsföring. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL HubSpot] koppling](connectors/marketing-automation/hubspot.md)

### Betalningar

Experience Platform stöder inmatning av data från tredje parts betalningssystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL PayPal] koppling](connectors/payments/paypal.md)

### Protokoll

Experience Platform har stöd för inmatning av data från tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [[!DNL Generic OData] koppling](connectors/protocols/odata.md)

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras inom Adobe Admin Console. Du kan få åtkomst till behörigheter via fliken **[!UICONTROL Permissions]** i en viss produktprofil. Från panelen **[!UICONTROL Edit Permissions]** kan du komma åt de behörigheter som gäller för källor via menyposten **[!UICONTROL data ingestion]**. **[!UICONTROL View Sources]**-behörigheten ger skrivskyddad åtkomst till tillgängliga källor på fliken **[!UICONTROL Catalog]** och autentiserade källor på fliken **[!UICONTROL Browse]**, medan behörigheten **[!UICONTROL Manage Sources]** ger fullständig åtkomst till att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **[!UICONTROL View Sources]** På | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken Katalog samt på flikarna Bläddra, Konton och Dataflöde. |
| **[!UICONTROL Manage Sources]** På | Förutom de funktioner som ingår i **[!UICONTROL View Sources]** ger åtkomst till alternativet **[!UICONTROL Connect Source]** i **[!UICONTROL Catalog]** och till alternativet **[!UICONTROL Select Data]** i **[!UICONTROL Browse]**. **[!UICONTROL Manage Sources]** kan du även aktivera eller inaktivera  **[!UICONTROL DataFlows]** och redigera deras scheman. |
| **[!UICONTROL View Sources]** Av och  **[!UICONTROL Manage Sources]** Av | Återkalla all åtkomst till källor. |

Mer information om tillgängliga behörigheter som beviljats via Admin Console, inklusive dessa fyra källor, finns i [översikten över åtkomstkontroll](../access-control/home.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som beta (&quot;Beta&quot;) bekräftar du härmed att betaversionen tillhandahålls ***som den är utan någon garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, ändra eller på annat sätt stödja betaversionen. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att betaversionen och/eller det medföljande materialet fungerar som de ska. Beta betraktas som konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om betaversionen, inklusive men inte begränsad till problem eller defekter som du stöter på när du använder betaversionen, förslag, förbättringar och rekommendationer) som du ger dig till Adobe tilldelas Adobe, inklusive alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
