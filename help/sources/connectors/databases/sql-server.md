---
keywords: Experience Platform;hem;populära ämnen;Microsoft SQL;microsoft sql;SQL;sql
solution: Experience Platform
title: SQL Server Source Connector - översikt
topic: översikt
description: Lär dig hur du ansluter Microsoft SQL Server till Adobe Experience Platform med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# (Beta) [!DNL Microsoft] SQL Server-koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Platform] kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasproviders inkluderar [!DNL Microsoft] SQL Server.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>SQL Server-källkopplingen [!DNL Microsoft] stöder för närvarande inte anslutning mellan flera regioner och plattformar. Det innebär att om din Azure-instans använder samma nätverksregion som plattformen går det inte att upprätta någon anslutning till plattformskällor. För närvarande stöds bara anslutning mellan regioner. Kontakta din kontoansvarige på Adobe för mer information.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Microsoft] SQL Server till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Microsoft] SQL Server till [!DNL Platform] med API:er

- [Skapa en Microsoft SQL Server-källanslutning med API:t för Flow Service](../../tutorials/api/create/databases/sql-server.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Microsoft] SQL Server till [!DNL Platform] med användargränssnittet

- [Skapa en Microsoft SQL Server-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/sql-server.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)