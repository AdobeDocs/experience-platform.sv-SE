---
keywords: Experience Platform;hem;populära ämnen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector - översikt
topic: översikt
description: Lär dig hur du ansluter Amazon Kinesis till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# (Beta) [!DNL Amazon Kinesis]-koppling

>[!NOTE]
>
>[!DNL Amazon Kinesis]-kopplingen är i betaversion. Se [Källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Du kan överföra data från dessa system till [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data till [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att ni kan hämta in data  [!DNL Amazon Kinesis] i realtid.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Anslut [!DNL Amazon Kinesis] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Kinesis] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Amazon Kinesis-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en källanslutning till Amazon Kinesis i användargränssnittet](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)