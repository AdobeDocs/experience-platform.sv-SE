---
keywords: Experience Platform;hem;populära ämnen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Översikt över källkopplingen för Oracle-objektlagring
topic: översikt
description: Lär dig hur du ansluter Oracle Object Storage till Adobe Experience Platform med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Oracle Object Storage-anslutning

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som AWS, [!DNL Google Cloud Platform], vilket gör att du kan överföra data från dessa system till Platform för användning i tjänster och destinationer längre fram i kedjan.

Lagringskällor i molnet kan hämta dina data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i källarbetsflödet. Med plattformen kan du hämta data från [!DNL Oracle Object Storage] via grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns i [IP-adressdokumentet tillåtelselista](../../ip-address-allow-list.md).

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen:

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, även om de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, t.ex. kontrolltecken (0x00 till 0x1F, \u0081 osv.). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Oracle Object Storage] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter Oracle Object Storage till Adobe Experience Platform med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en källanslutning för Oracle Object Storage med API:t för Flow Service](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en källanslutning för Oracle-objektlagring i användargränssnittet](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)