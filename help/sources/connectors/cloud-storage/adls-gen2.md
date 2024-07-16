---
title: Azure Data Lake Storage Gen2 Source Connector - översikt
description: Lär dig hur du ansluter Azure Data Lake Storage Gen2 till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: f879f2a627e55db96a89796b9f3308744bf93f67
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2-anslutning

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure], vilket gör att du kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data till Experience Platform utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Med Experience Platform kan du hämta data från [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) via grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Källan [!DNL Azure Data Lake Storage Gen2] stöder inte anslutning mellan flera regioner och Experience Platform. Om din Azure-instans använder samma nätverksregion som Experience Platform går det inte att upprätta någon anslutning till Experience Platform-källor. Använd inte regionerna Azure East US 2, Azure West Europe och Azure Australia East när du konfigurerar din [!DNL Azure Data Lake Storage Gen2]-källa. För närvarande stöds bara anslutning mellan regioner.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Anslut [!DNL Azure Data Lake Storage Gen2] till Experience Platform

>[!NOTE]
>
>Tjänstens huvudnamn som används för att skapa ett [!DNL Azure Data Lake Storage Gen2]-konto måste ha minst rollen **Lagringsblobbdata Reader** tilldelad från åtkomstkontrollen (IAM)

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Data Lake Storage Gen2] till Experience Platform med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en  [!DNL Azure Data Lake Storage Gen2] basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en  [!DNL Azure Data Lake Storage Gen2] källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
