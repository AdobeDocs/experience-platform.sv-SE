---
keywords: Experience Platform;hem;populära ämnen;HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: Apache HDFS Source Connector - översikt
description: Lär dig hur du ansluter Apache HDFS till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# (Beta) [!DNL Apache] HDFS-anslutning

>[!NOTE]
>
>Apache HDFS-kontakten är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../home.md#terms-and-conditions).

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure], vilket gör att du kan hämta data från dessa system. Inkapslade data kan formateras som JSON, Parquet eller avgränsade. Stöd för molnlagringsleverantörer inkluderar [!DNL Apache] HDFS.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Anslut [!DNL Apache] HDFS till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Apache] HDFS till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en HDFS-basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Apache HDFS-källanslutning i gränssnittet](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
