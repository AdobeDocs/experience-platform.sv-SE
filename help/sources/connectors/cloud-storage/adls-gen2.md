---
keywords: Experience Platform;hem;populära ämnen;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Översikt över Azure Data Lake Storage Gen2 Source Connector
topic-legacy: overview
description: Lär dig hur du ansluter Azure Data Lake Storage Gen2 till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 72c3000022db68284836cc7f2248154493100913
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2-anslutning

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta in data från dessa system.

Lagringskällor i molnet kan överföra egna data till [!DNL Platform] utan att behöva ladda ned, formatera eller ladda upp. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] låter dig hämta in data från [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) genom grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

>[!IMPORTANT]
>
>The [!DNL Azure Data Lake Storage Gen2] Källan stöder inte anslutning till Experience Platform mellan flera regioner. Om din Azure-instans använder samma nätverksregion som Experience Platform går det inte att upprätta någon anslutning till Experience Platform-källor. Använd inte regionerna Azure East US 2, Azure West Europe och Azure Australia East när du konfigurerar [!DNL Azure Data Lake Storage Gen2] källa. För närvarande stöds bara anslutning mellan regioner.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Azure Data Lake Storage Gen2] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Azure Data Lake Storage Gen2] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en ADLS-Gen2-basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en ADLS-Gen2-källanslutning i gränssnittet](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
