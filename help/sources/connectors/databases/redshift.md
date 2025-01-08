---
title: Amazon Redshift Source Connector - översikt
description: Lär dig hur du ansluter Amazon Redshift till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: dbeeab9182ae67e5c9c691707faeddf04f4e94b2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# [!DNL Amazon Redshift]-källa

>[!IMPORTANT]
>
>Källan [!DNL Amazon Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för att importera data från en tredjepartsdatabas. Plattformen kan ansluta till olika typer av databaser, till exempel relationsdatabaser, NoSQL-databaser eller datalager. Stöd för databasproviders är [!DNL Amazon Redshift].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Konfigurera din [!DNL Amazon Redshift]-källa för Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](../../../landing/multi-cloud.md).

Lägg till följande IP-adresser i tillåtelselista för att ansluta ditt [!DNL Amazon Redshift]-konto till Experience Platform på Amazon Web Services (AWS):

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

## Anslut [!DNL Amazon Redshift] till plattformen med API:er

- [Skapa en Amazon Redshift-basanslutning med API:t för Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Amazon Redshift] till plattformen med användargränssnittet

- [Skapa en Amazon Redshift-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/redshift.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
