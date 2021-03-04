---
keywords: Experience Platform;hem;populära ämnen;Google PubSub;google pubsub
solution: Experience Platform
title: Google PubSub Source Connector - översikt
topic: översikt
description: Lär dig hur du ansluter Google PubSub till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (Beta) [!DNL Google PubSub]-koppling

>[!NOTE]
>
>[!DNL Google PubSub]-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [källöversikten](../../home.md#terms-and-conditions).

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som [!DNL AWS], [!DNL Google Cloud Platform] och [!DNL Azure], vilket gör att du kan överföra data från dessa system till plattformen för användning i underordnade tjänster och mål.

Lagringskällor i molnet kan hämta dina data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i källarbetsflödet. Med hjälp av plattformen kan du hämta data från [!DNL Azure Event Hubs] i realtid.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Anslut [!DNL Google PubSub] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google PubSub] till plattformen med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google PubSub-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en Google PubSub-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)