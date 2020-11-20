---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Azure Event Hubs-koppling
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter Azure Event Hubs till plattformen med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: c0c609e3f385665cf88129def0c69e7d153ce201
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# (Beta) Azure Event Hubs-anslutning

>[!NOTE]
>
>Azure Event Hubs-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]. Ni kan föra in data från dessa system i [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] kan ni hämta in data från [!DNL Azure Event Hubs] i realtid.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md) .

## Anslut [!DNL Azure Event Hubs] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Event Hubs] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Azure Event Hubs-koppling med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en Azure Event Hubs-källkoppling i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)