---
keywords: Experience Platform;hem;populära ämnen;Azure Table Storage;azure table storage;ATS;ats
solution: Experience Platform
title: Översikt över Azure Table Storage Source Connector
topic-legacy: overview
description: Lär dig hur du ansluter Azure Table Storage till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# (Beta) [!DNL Azure Table Storage]-koppling

>[!NOTE]
>
>[!DNL Azure Table Storage]-kopplingen är i betaversion. Se [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform]-tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Platform] kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasproviders är [!DNL Azure Table Storage].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>[!DNL Azure Table Storage]-källkopplingen stöder för närvarande inte anslutning mellan flera regioner och plattformar. Det innebär att om din Azure-instans använder samma nätverksregion som plattformen går det inte att upprätta någon anslutning till plattformskällor. För närvarande stöds bara anslutning mellan regioner. Kontakta din kontoansvarige på Adobe för mer information.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Table Storage] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Azure Table Storage] till [!DNL Platform] med API:er

- [Skapa en Azure Table Storage-källanslutning med API:t för Flow Service](../../tutorials/api/create/databases/ats.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Azure Table Storage] till [!DNL Platform] med användargränssnittet

- [Skapa en Azure Table Storage-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/ats.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
