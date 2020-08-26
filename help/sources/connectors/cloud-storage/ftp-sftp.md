---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FTP- och SFTP-anslutning
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# (Beta) FTP- och SFTP-anslutning

>[!NOTE]
>
>FTP- och SFTP-anslutningarna är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att du kan hämta data från en FTP- eller SFTP-server via grupper.

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

Dokumentationen nedan innehåller information om hur du ansluter en FTP- eller STFP-server till [!DNL Platform] API:er eller användargränssnittet:

## Koppla FTP och SFTP till [!DNL Platform] API:er

- [Skapa en FTP- eller SFTP-anslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/sftp.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

## Ansluta FTP eller SFTP till [!DNL Platform] användargränssnittet

- [Skapa en FTP- eller SFTP-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/ftp-sftp.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)