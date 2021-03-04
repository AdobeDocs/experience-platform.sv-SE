---
keywords: Experience Platform;hem;populära ämnen;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Översikt över Azure Event Hubs Source Connector
topic: översikt
description: Lär dig hur du ansluter Azure Event Hubs till Adobe Experience Platform med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# (Beta) Azure Event Hubs-anslutning

>[!NOTE]
>
>Azure Event Hubs-kopplingen är i betaversion. Se [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Du kan överföra data från dessa system till [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data till [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att ni kan hämta in data  [!DNL Azure Event Hubs] i realtid.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Anslut [!DNL Azure Event Hubs] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Event Hubs] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Azure Event Hubs-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en Azure Event Hubs-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)