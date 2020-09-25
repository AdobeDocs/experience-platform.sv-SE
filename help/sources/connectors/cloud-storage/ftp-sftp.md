---
keywords: Experience Platform;home;popular topics;FTP;SFTP;ftp;sftp
solution: Experience Platform
title: FTP- och SFTP-anslutning
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter en FTP- eller STFP-server till plattformen med API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 93584ecbbe3be40c6ebee09cac85d497e4a99317
workflow-type: tm+mt
source-wordcount: '476'
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

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`är ogiltiga i NTFS-filnamn, men som inte är giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut FTP och SFTP till [!DNL Platform]

>[!IMPORTANT]
>
>Användarna måste inaktivera interaktiv tangentbordsautentisering i SFTP-serverkonfigurationen innan de ansluter. Om du inaktiverar inställningen kan du ange lösenord manuellt, i stället för att skriva in via en tjänst eller ett program. Mer information om interaktiv autentisering för tangentbord finns i [Component Pro-dokumentet](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) .

Dokumentationen nedan innehåller information om hur du ansluter en FTP- eller SFTP-server till [!DNL Platform] API:er eller användargränssnittet:

### Använda API:er

- [Skapa en FTP- eller SFTP-anslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/sftp.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en FTP- eller SFTP-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/ftp-sftp.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)