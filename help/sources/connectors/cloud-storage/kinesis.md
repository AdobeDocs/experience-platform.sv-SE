---
keywords: Experience Platform;home;popular topics;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Connector
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter Amazon Kinesis till plattformen med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 7b92327cfeb2410baf313dd650f68cfeb6db36e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# (Beta)- [!DNL Amazon Kinesis] anslutning

>[!NOTE]
>
>Kopplingen [!DNL Amazon Kinesis] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]. Ni kan föra in data från dessa system i [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] kan ni hämta in data från [!DNL Amazon Kinesis] i realtid.

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

## Anslut [!DNL Amazon Kinesis] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Kinesis] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Amazon Kinesis-anslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Amazon Kinesis-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)