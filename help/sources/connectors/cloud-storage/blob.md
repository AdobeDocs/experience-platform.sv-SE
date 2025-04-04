---
keywords: Experience Platform;home;populära topics;Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob Source Connector - översikt
description: Lär dig hur du ansluter Azure Blob till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Azure Blob-koppling

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Du kan hämta data från dessa system till [!DNL Experience Platform].

Molnlagringskällor kan hämta dina egna data till [!DNL Experience Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Med [!DNL Experience Platform] kan du hämta data från [!DNL Azure Blob] via grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Källan [!DNL Azure Blob] stöder inte anslutning mellan flera regioner och Experience Platform. Om din [!DNL Azure]-instans använder samma nätverksregion som Experience Platform går det inte att upprätta någon anslutning till Experience Platform-källor. För närvarande stöds bara anslutning mellan regioner.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Anslut [!DNL Azure Blob] till [!DNL Experience Platform]

Dokumentationen nedan innehåller information om hur du ansluter Azure Blob till Adobe Experience Platform med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Azure Blob-basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/blob.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Azure Blob-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/blob.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
