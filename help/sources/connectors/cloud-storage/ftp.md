---
keywords: Experience Platform;hem;populära ämnen;FTP;ftp;
solution: Experience Platform
title: Översikt över FTP-källkoppling
description: Lär dig hur du ansluter en FTP-server till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (Beta) FTP-anslutning

>[!NOTE]
>
>FTP-kopplingen är i betaversion. Se [Översikt över källor](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta in data från dessa system.

Lagringskällor i molnet kan överföra egna data till [!DNL Platform] utan att behöva ladda ned, formatera eller ladda upp. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att du kan hämta data från en FTP- eller SFTP-server via grupper.

>[!IMPORTANT]
>
>När du skapar ett dataflöde med FTP-källkopplingen bör du ställa in ett engångsschema på grund av kvarstående problem med inkrementella uppdateringar som påträffas i FTP-servrar.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut FTP till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter en FTP-server till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en FTP-basanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/ftp.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en FTP-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/ftp.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
