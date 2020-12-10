---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: SFTP-anslutning
topic: overview
description: Dokumentationen nedan innehåller information om hur du ansluter en SFTP-server till plattformen med hjälp av API:er eller användargränssnittet.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# (Beta) SFTP-anslutning

>[!NOTE]
>
>SFTP-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../home.md#terms-and-conditions) .

Adobe Experience Platform erbjuder inbyggd anslutningsbarhet för molnleverantörer som AWS [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM-parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att du kan hämta data från en FTP- eller SFTP-server via grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md) .

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`är ogiltiga i NTFS-filnamn, men som inte är giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut SFTP till [!DNL Platform]

>[!IMPORTANT]
>
>Användarna måste inaktivera interaktiv tangentbordsautentisering i SFTP-serverkonfigurationen innan de ansluter. Om du inaktiverar inställningen kan du ange lösenord manuellt, i stället för att skriva in via en tjänst eller ett program. Mer information om interaktiv autentisering för tangentbord finns i [Component Pro-dokumentet](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) .

Dokumentationen nedan innehåller information om hur du ansluter en SFTP-server till [!DNL Platform] API:er eller användargränssnittet:

### Använda API:er

- [Skapa en SFTP-anslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/sftp.md)
- [Utforska ett molnlagringssystem med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Samla in molnlagringsdata med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en SFTP-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Konfigurera ett dataflöde för en molnlagringskontakt i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)