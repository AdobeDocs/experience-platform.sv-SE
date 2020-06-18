---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Source Connectors - översikt
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---


# Översikt över källkopplingar

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får för att göra mer.

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program

Experience Platform tillåter att data hämtas från andra Adobe-program, inklusive Adobe Analytics, Adobe Audience Manager och Experience Platform Launch. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager-anslutning - översikt](connectors/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Översikt över Adobe Analytics dataanslutning](connectors/adobe-applications/analytics.md)
- [Skapa en Adobe Analytics-källanslutning i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Skapa en källkoppling för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reklam

Experience Platform stöder inmatning av data från ett annonssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Google AdWords-koppling](connectors/advertising/ads.md)

### molnlagring

Lagringskällor i molnet kan överföra dina egna data till Platform utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

- [Azure Data Lake Storage Gen2-anslutning](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob och Amazon S3-kontakt](connectors/cloud-storage/blob-s3.md)
- [Amazon Kinesis-kontakt](connectors/cloud-storage/kinesis.md)
- [Apache HDFS-kontakt](connectors/cloud-storage/hdfs.md)
- [Azure Event Hubs-koppling](connectors/cloud-storage/eventhub.md)
- [Azure File Storage Connector](connectors/cloud-storage/azure-file-storage.md)
- [FTP- och SFTP-anslutning](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud Storage Connector](connectors/cloud-storage/google-cloud-storage.md)

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från Microsoft Dynamics 365 och Salesforce. Mer information finns i följande relaterade dokument:

- [Microsoft Dynamics-anslutning](connectors/crm/ms-dynamics.md)
- [Salesforce-koppling](connectors/crm/salesforce.md)

### Nöjda kunder

Experience Platform har stöd för inhämtning av data från tredjepartsprogram. Mer information finns i följande relaterade dokument:

- [Salesforce Service Cloud-anslutning](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow-koppling](connectors/customer-success/servicenow.md)

### Databas

Experience Platform har stöd för att importera data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Amazon Redshift-kontakt](connectors/databases/redshift.md)
- [Apache Hive på Azure HDInsights-kontakten](connectors/databases/hive.md)
- [Apache Spark på Azure HDInsights-kontakten](connectors/databases/spark.md)
- [Azure Data Explorer-koppling](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics Connector](connectors/databases/synapse-analytics.md)
- [Azure Table Storage-koppling](connectors/databases/ats.md)
- [Koppling till kuchbase](connectors/databases/couchbase.md)
- [Google BigQuery-koppling](connectors/databases/bigquery.md)
- [GreenPlum-kontakt](connectors/databases/greenplum.md)
- [HP Vertica-koppling](connectors/databases/hp-vertica.md)
- [IBM DB2-anslutning](connectors/databases/ibm-db2.md)
- [MariaDB-koppling](connectors/databases/mariadb.md)
- [Microsoft SQL Server-anslutning](connectors/databases/sql-server.md)
- [MySQL-koppling](connectors/databases/mysql.md)
- [Oracle-koppling](connectors/databases/oracle.md)
- [Phoenix-kontakt](connectors/databases/phoenix.md)
- [PostgreSQL-koppling](connectors/databases/postgres.md)

### Marknadsföringsautomatisering

Experience Platform stöder inmatning av data från ett system för automatisering av tredjepartsmarknadsföring. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [HubSpot-anslutning](connectors/marketing-automation/hubspot.md)

### Betalningar

Experience Platform stöder inmatning av data från tredje parts betalningssystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [PayPal-anslutning](connectors/payments/paypal.md)

### Protokoll

Experience Platform har stöd för inmatning av data från tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Allmän OData-koppling](connectors/protocols/odata.md)

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras i Adobe Admin Console. Du kan få åtkomst till behörigheter via fliken *Behörigheter* i en viss produktprofil. Från panelen **Redigera behörigheter** kan du komma åt de behörigheter som gäller för källor via menyposten för *dataöverföring* . Behörigheten **Visa källor** ger skrivskyddad åtkomst till tillgängliga källor på fliken *Katalog* och autentiserade källor på fliken *Bläddra* , medan behörigheten **Hantera källor** ger fullständig åtkomst till att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **Visa källor** på | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken *Katalog* , samt flikarna *Bläddra*, *Konton* och *DataFlow* . |
| **Hantera källor** på | Förutom de funktioner som ingår i **Visa källor** ger åtkomst till alternativet *Anslut källa* i *katalog* och till alternativet *Välj data* i *Bläddra*. **Med Hantera källor** kan du även aktivera eller inaktivera *DataFlow* och redigera deras scheman. |
| **Visa källor** av och **hantera källor** av | Återkalla all åtkomst till källor. |

Mer information om de behörigheter som ges via Admin Console, inklusive dessa fyra källor, finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Villkor {#terms-and-conditions}

Genom att använda någon av källorna som är märkta som beta (&quot;Beta&quot;) bekräftar du härmed att betaversionen tillhandahålls ***&quot;som den är&quot; utan någon garanti av något slag***.

Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt ge support för betaversionen. Du rekommenderas att vara försiktig och inte på något sätt förlita dig på att betaversionen och/eller det medföljande materialet fungerar som de ska. Beta betraktas som Konfidentiell information om Adobe.

All &quot;Feedback&quot; (information om betaversionen, inklusive men inte begränsad till problem eller defekter som du råkat ut för när du använt betaversionen, förslag, förbättringar och rekommendationer) som du fått från dig till Adobe, tilldelas härmed Adobe med alla rättigheter, titlar och intressen i och för sådan feedback.

Skicka Öppna feedback eller skapa en supportanmälan för att dela dina förslag eller rapportera ett fel, sök efter en funktionsförbättring.
