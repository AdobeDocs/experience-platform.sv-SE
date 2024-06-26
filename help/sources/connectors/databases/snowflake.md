---
title: Snowflake Source Connector - översikt
description: Lär dig hur du ansluter Snowflake till Adobe Experience Platform med API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake] källa

>[!IMPORTANT]
>
>* The [!DNL Snowflake] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.
>* Som standard är [!DNL Snowflake] källtolkningar `null` som en tom sträng. Kontakta din Adobe-representant för att säkerställa att `null` värden skrivs korrekt som `null` i Adobe Experience Platform.
>* För att Experience Platform ska kunna importera data måste tidszoner för alla tabellbaserade batchkällor konfigureras till UTC. Den enda tidsstämpeln som stöds för [!DNL Snowflake] källan är TIMESTAMP_NTZ med UTC-tid.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för att importera data från en tredjepartsdatabas. Plattformen kan ansluta till olika typer av databaser, till exempel relationsdatabaser, NoSQL-databaser eller datalager. Stöd för databasleverantörer innefattar [!DNL Snowflake].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Snowflake] till Plattform med API:er eller användargränssnittet:

## Anslut [!DNL Snowflake] till plattform med API:er

* [Skapa en Snowflake-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Snowflake] till plattform med användargränssnittet

* [Skapa en Snowflake-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/snowflake.md)
* [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
