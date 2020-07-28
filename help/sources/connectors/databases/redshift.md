---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Amazon Redshift-anslutning
topic: overview
translation-type: tm+mt
source-git-commit: 3b5e76afea5689dbd59f64f6192e6ef2a6acb7d3
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---


# (Beta)- [!DNL Amazon Redshift] anslutning

>[!NOTE]
>Kopplingen [!DNL Amazon Redshift] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform tillåter att data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

[!DNL Experience Platform] har stöd för inmatning av data från en tredjepartsdatabas. [!DNL Platform] kan ansluta till olika typer av databaser, till exempel relational, NoSQL eller data warehouse. Stöd för databasleverantörer är bland annat [!DNL Amazon Redshift].

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

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Redshift] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Amazon Redshift] till [!DNL Platform] med API:er

- [Skapa en Amazon Redshift-koppling med API:t för Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Ansluta [!DNL Amazon Redshift] till [!DNL Platform] användargränssnittet

- [Skapa en Amazon Redshift-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/redshift.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)