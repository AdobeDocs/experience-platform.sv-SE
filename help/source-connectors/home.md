---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Source Connectors - översikt
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# Översikt över källkopplingar

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som ni kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar till olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dina tredjepartssystem, ange tider för att få tillgång till dem och hantera dataöverföringshastigheten.

Med Experience Platform kan ni centralisera data som ni samlar in från olika källor och använda de insikter ni får av den för att göra mer.

## Typer av källor

Källor i Experience Platform är grupperade i följande kategorier:

### Adobe-program

Med Experience Platform kan data hämtas från andra Adobe-program, inklusive Adobe Analytics, Adobe Audience Manager och Experience Platform Launch. Mer information finns i följande relaterade dokument:

- [Adobe Audience Manager connector overview](./ui/adobe-applications/audience-manager.md)
- [Skapa en Adobe Audience Manager-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Översikt över Adobe Analytics-dataanslutning](./ui/adobe-applications/analytics.md)
- [Skapa en källanslutning för Adobe Analytics i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### molnlagring

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Varje steg i processen integreras i arbetsflödet Källor med användargränssnittet. Stöd för molnlagringsleverantörer omfattar Amazon S3, Azure Blob, FTP-servrar och SFTP-servrar. Mer information finns i följande relaterade dokument:

- [Skapa en Azure Blob- eller Amazon S3-källanslutning i gränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [Skapa en Azure Data Lake Storage Gen2-källanslutning i gränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [Skapa en FTP- eller SFTP-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [Skapa en Google Cloud-källanslutning för lagring i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### CRM (Customer Relationship Management)

CRM-system tillhandahåller data som kan hjälpa till att bygga upp kundrelationer, vilket i sin tur skapar lojalitet och driver kundlojalitet. Experience Platform har stöd för att importera CRM-data från Microsoft Dynamics 365 och Salesforce. Mer information finns i följande relaterade dokument:

- [Skapa en Microsoft Dynamics 365- eller Salesforce-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [Skapa en PayPal-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### Nöjda kunder (CS)

Experience Platform har stöd för inmatning av data från en tredjepartsapp för kundframgångar. Mer information finns i följande relaterade dokument:

- [Skapa en Salesforce Service Cloud-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [Skapa en ServiceNow-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### Databas

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Skapa en källanslutning för AWS Redshift i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [Skapa en Azure Synapse Analytics-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [Skapa en Google BigQuery-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [Skapa en MariaDB-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [Skapa en Microsoft SQL Server-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [Skapa en MySQL-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [Skapa en PostgreSQL-källkoppling i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### Marknadsföringsautomatisering

Experience Platform har stöd för inmatning av data från ett system för automatiserad marknadsföring från tredje part. Mer information om specifika källanslutningar finns i följande relaterade dokument:

- [Skapa en HubSpot-källanslutning i användargränssnittet](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## API-självstudiekurser

Du kan skapa källanslutningar med API:t för Flow Service. Mer information finns i självstudiekursen om [källor-API](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md).

## Åtkomstkontroll för källor vid datainhämtning

Behörigheter för källor vid dataöverföring kan hanteras i Adobe Admin Console. Du kan få åtkomst till behörigheter via fliken *Behörigheter* i en viss produktprofil. Från panelen **Redigera behörigheter** kan du komma åt de behörigheter som gäller för källor via menyposten för *dataöverföring* . Behörigheten **Visa källor** ger skrivskyddad åtkomst till tillgängliga källor på fliken *Katalog* och autentiserade källor på fliken *Bläddra* , medan behörigheten **Hantera källor** ger fullständig åtkomst till att läsa, skapa, redigera och inaktivera källor.

Följande tabell visar hur användargränssnittet beter sig baserat på olika kombinationer av dessa behörigheter:

| Behörighetsnivå | Beskrivning |
| ---- | ----|
| **Visa källor** på | Ge skrivskyddad åtkomst till källor i varje källtyp på fliken *Katalog* , samt flikarna *Bläddra*, *Konton* och *DataFlow* . |
| **Hantera källor** på | Förutom de funktioner som ingår i **Visa källor** ger åtkomst till alternativet *Anslut källa* i *katalog* och till alternativet *Välj data* i *Bläddra*. **Med Hantera källor** kan du även aktivera eller inaktivera *DataFlow* och redigera deras scheman. |
| **Visa källor** av och **hantera källor** av | Återkalla all åtkomst till källor. |

Mer information om de behörigheter som ges via Admin Console, inklusive dessa fyra källor, finns i [åtkomstkontrollsöversikten](../access-control/home.md).
