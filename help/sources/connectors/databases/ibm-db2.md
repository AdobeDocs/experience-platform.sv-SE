---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: IBM DB2-anslutning
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# (Beta) IBM DB2-anslutning

>[!NOTE]
>
>IBM DB2-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för databasleverantörer som [!DNL Microsoft], MySQL och [!DNL Azure]. Ni kan föra in data från dessa system i [!DNL Platform].

Olika typer av tredjepartsdatabaser stöds, bland annat relational, NoSQL och data warehouse. Stöd för databasleverantörer inkluderar IBM DB2.

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

Dokumentationen nedan innehåller information om hur du ansluter IBM DB2 till [!DNL Platform] API:er eller användargränssnittet:

## Koppla IBM DB2 till [!DNL Platform] API:er

- [Skapa en IBM DB2-anslutning med API:t för Flow Service](../../tutorials/api/create/databases/ibm-db2.md)
- [Utforska ett databassystem med API:t för Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Samla in data från en databas med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut IBM DB2 till [!DNL Platform] användargränssnittet

- [Skapa en IBM DB2-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/ibm-db2.md)
- [Konfigurera ett dataflöde för en databasanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)