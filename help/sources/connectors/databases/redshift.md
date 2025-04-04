---
title: Amazon Redshift Source Connector - översikt
description: Lär dig hur du ansluter Amazon Redshift till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# [!DNL Amazon Redshift]-källa

>[!IMPORTANT]
>
>- Källan [!DNL Amazon Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.
>
>- Du kan nu använda källan [!DNL Amazon Redshift] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).


Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från en tredjepartsdatabas. Experience Platform kan ansluta till olika typer av databaser, till exempel relationsdatabaser, NoSQL-databaser eller datalager. Stöd för databasproviders är [!DNL Amazon Redshift].

## Konfigurera din [!DNL Amazon Redshift]-källa för Experience Platform på Azure {#azure}

Följ stegen nedan för att lära dig hur du kan konfigurera ditt [!DNL Amazon Redshift]-konto för Experience Platform på Azure.

### IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Konfigurera din [!DNL Amazon Redshift]-källa för Experience Platform på Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).

### IP-adressen tillåtelselista för anslutning till AWS

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform på AWS. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform på AWS](../../ip-address-allow-list.md).

## Anslut [!DNL Amazon Redshift] till Experience Platform med API:er

- [Anslut Amazon Redshift till Experience Platform med API:t för Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en datakälla med API:t för Flow Service](../../tutorials/api/collect/database-nosql.md)

## Anslut [!DNL Amazon Redshift] till Experience Platform med användargränssnittet

- [Skapa en Amazon Redshift-källanslutning i användargränssnittet](../../tutorials/ui/create/databases/redshift.md)
- [Skapa ett dataflöde för en datakällanslutning i användargränssnittet](../../tutorials/ui/dataflow/databases.md)
