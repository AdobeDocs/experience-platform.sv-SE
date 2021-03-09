---
keywords: Experience Platform;hem;populära ämnen;Azure Data Explorer;azure data explorer
solution: Experience Platform
title: Översikt över Azure Data Explorer Source Connector
topic: översikt
description: Lär dig hur du ansluter Azure-Data Explorer till Adobe Experience Platform med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# (Beta) [!DNL Azure Data Explorer]-koppling

>[!NOTE]
>
>[!DNL Azure Data Explorer]-kopplingen är i betaversion. Se [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Adobe Experience Platform erbjuder systemspecifik anslutning för databasleverantörer som [!DNL Microsoft], MySQL och [!DNL Azure]. Du kan överföra data från dessa system till [!DNL Platform].

Olika typer av tredjepartsdatabaser stöds, bland annat relational, NoSQL och data warehouse. Stöd för databasproviders inkluderar [!DNL Azure Data Explorer].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>[!DNL Azure Data Explorer]-källkopplingen stöder för närvarande inte anslutning mellan flera regioner och plattformar. Det innebär att om din Azure-instans använder samma nätverksregion som plattformen går det inte att upprätta någon anslutning till plattformskällor. För närvarande stöds bara anslutning mellan regioner. Kontakta din kontoansvarige på Adobe för mer information.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Data Explorer] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Azure Data Explorer] till [!DNL Platform] med API:er

- [Skapa en Azure Data Explorer-källanslutning med API:t för Flow Service](../../tutorials/api/create/databases/data-explorer.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Azure Data Explorer] till [!DNL Platform] med användargränssnittet

- [Skapa en Azure Data Explorer-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/data-explorer.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)