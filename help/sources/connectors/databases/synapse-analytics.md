---
keywords: Experience Platform;hem;populära ämnen;Azure synapse Analytics;azure synapse analytics;Synapse;synapse
solution: Experience Platform
title: azure synapse Analytics Source Connector - översikt
topic-legacy: overview
description: Lär dig hur du ansluter Azure synapse Analytics till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics] koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Platform] kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasproviders är [!DNL Azure Synapse Analytics].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]-källkopplingen stöder för närvarande inte anslutning mellan flera regioner och plattformar. Det innebär att om din Azure-instans använder samma nätverksregion som plattformen går det inte att upprätta någon anslutning till plattformskällor. För närvarande stöds bara anslutning mellan regioner. Kontakta din kontoansvarige på Adobe för mer information.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Synapse Analytics] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Azure Synapse Analytics] till [!DNL Platform] med API:er

- [Skapa en Azure synapse Analytics-källanslutning med API:t för Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Azure Synapse Analytics] till [!DNL Platform] med användargränssnittet

- [Skapa en Azure synapse Analytics-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
