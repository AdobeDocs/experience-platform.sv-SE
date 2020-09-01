---
keywords: Experience Platform;home;popular topics;PostgreSQL;postgresql
solution: Experience Platform
title: PostgreSQL-koppling
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter PostgreSQL till plattformen med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# (Beta)- [!DNL PostgreSQL] anslutning

>[!NOTE]
>
>Kopplingen [!DNL PostgreSQL] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Platform] kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasleverantörer är bland annat [!DNL PostgreSQL].

## IP-adress tillåtelselista

Följande IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor.

### USA, östra

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Västeuropa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australien, östra

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

Dokumentationen nedan innehåller information om hur du ansluter [!DNL PostgreSQL] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL PostgreSQL] till [!DNL Platform] med API:er

- [Skapa en PostgreSQL-koppling med API:t för Flow Service](../../tutorials/api/create/databases/postgres.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Ansluta [!DNL PostgreSQL] till [!DNL Platform] användargränssnittet

- [Skapa en PostgreSQL-källkoppling i användargränssnittet](../../tutorials/ui/create/databases/postgres.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)