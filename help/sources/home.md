---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Source Connectors - översikt
topic: overview
translation-type: tm+mt
source-git-commit: 8ee88b27c79610827ff2627999e303b5fc43e1c6

---


# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får av den för att göra mer.

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program

Med Experience Platform kan data hämtas från andra Adobe-program, inklusive Adobe Analytics, Adobe Audience Manager och Experience Platform Launch. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager connector overview](connectors/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källkoppling i användargränssnittet](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Översikt över Adobe Analytics-dataanslutning](connectors/adobe-applications/analytics.md)
- [Skapa en källanslutning för Adobe Analytics i användargränssnittet](./tutorials/ui/create/adobe-applications/analytics.md)
- [Skapa en källkoppling för kundattribut i användargränssnittet](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Reklam

Experience Platform har stöd för inmatning av data från ett annonssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Google Ads-koppling](connectors/advertising/ads.md)

### molnlagring

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Mer information finns i följande relaterade dokument:

- [Azure Data Lake Storage Gen2-anslutning](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob och Amazon S3-kontakt](connectors/cloud-storage/blob-s3.md)
- [FTP- och SFTP-anslutning](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud Storage Connector](connectors/cloud-storage/google-cloud-storage.md)

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från Microsoft Dynamics 365 och Salesforce. Mer information finns i följande relaterade dokument:

- [Microsoft Dynamics-anslutning](connectors/crm/ms-dynamics.md)
- [Salesforce-koppling](connectors/crm/salesforce.md)

### Nöjda kunder

Experience Platform har stöd för inmatning av data från en tredjepartsapp för kundframgångar. Mer information finns i följande relaterade dokument:

- [Salesforce Service Cloud-anslutning](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow-koppling](connectors/customer-success/servicenow.md)

### Databas

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Amazon Redshift-kontakt](connectors/databases/redshift.md)
- [Apache Hive på Azure HDInsights-kontakten](connectors/databases/hive.md)
- [Apache Spark på Azure HDInsights-kontakten](connectors/databases/spark.md)
- [Azure Data Explorer-koppling](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics-koppling](connectors/databases/synapse-analytics.md)
- [Azure Table Storage-koppling](connectors/databases/ats.md)
- [Google BigQuery-koppling](connectors/databases/bigquery.md)
- [IBM DB2-anslutning](connectors/databases/ibm-db2.md)
- [MariaDB-koppling](connectors/databases/mariadb.md)
- [Microsoft SQL Server-anslutning](connectors/databases/sql-server.md)
- [MySQL-koppling](connectors/databases/mysql.md)
- [Oracle-koppling](connectors/databases/oracle.md)
- [Phoenix-kontakt](connectors/databases/phoenix.md)
- [PostgreSQL-koppling](connectors/databases/postgres.md)

### Marknadsföringsautomatisering

Experience Platform har stöd för inmatning av data från ett system för automatiserad marknadsföring från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [HubSpot-anslutning](connectors/marketing-automation/hubspot.md)

### Betalningar

Experience Platform har stöd för inmatning av data från ett betalningssystem från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [PayPal-anslutning](connectors/payments/paypal.md)

### Protokoll

Experience Platform har stöd för inmatning av data från ett tredjepartsprotokollsystem. Mer information om specifika källanslutningar finns i följande relaterade dokument:

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
