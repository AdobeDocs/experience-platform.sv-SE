---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Azure Event Hubs-koppling
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter Azure Event Hubs till plattformen med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# (Beta) Azure Event Hubs-anslutning

>[!NOTE]
>
>Azure Event Hubs-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]. Ni kan föra in data från dessa system i [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] kan ni hämta in data från [!DNL Azure Event Hubs] i realtid.

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

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Event Hubs] till [!DNL Platform] med API:er eller användargränssnittet:

## Anslut [!DNL Azure Event Hubs] till [!DNL Platform] med API:er

- [Skapa en Azure Event Hubs-koppling med API:t för Flow Service](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

## Ansluta [!DNL Azure Event Hubs] till [!DNL Platform] användargränssnittet

- [Skapa en Azure Event Hubs-källkoppling i användargränssnittet](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)