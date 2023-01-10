---
keywords: Experience Platform;hem;populära ämnen;Google Cloud Storage;Google cloud storage
solution: Experience Platform
title: Google Cloud Storage Source Connector - översikt
description: Lär dig hur du ansluter Google Cloud-lagring till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Google Cloud Storage Connector

Adobe Experience Platform erbjuder anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform]och [!DNL Azure]så att ni kan hämta in data från dessa system.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som JSON eller Parquet som är kompatibelt med Experience Data Model (XDM), eller i ett avgränsat format. Varje steg i processen är integrerat i källarbetsflödet. Plattformen gör att du kan hämta in data från [!DNL Google Cloud Storage] genom grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar för att ansluta [!DNL Google Cloud Storage] konto

För att kunna ansluta till plattformen måste du först aktivera interoperabilitet för [!DNL Google Cloud Storage] konto. Öppna för att få åtkomst till inställningen för interoperabilitet [!DNL Google Cloud Platform] och markera **[!UICONTROL Settings]** från **[!UICONTROL Cloud Storage]** i navigeringspanelen.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

The **[!UICONTROL Settings]** visas. Här kan du se information om [!DNL Google] projekt-ID och information om [!DNL Google Cloud Storage] konto. Välj **[!UICONTROL Interoperability]** i det övre sidhuvudet.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

The **[!UICONTROL Interoperability]** sidan innehåller information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt tjänstkonto. Om du vill generera ett nytt åtkomstnyckel-ID och en hemlig åtkomstnyckel för ditt tjänstkonto väljer du **[!UICONTROL Create a Key for a Service Account]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade ID för åtkomstnyckel och hemlig åtkomstnyckel för att ansluta din [!DNL Google Cloud Storage] konto till plattform.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Google Cloud Storage] till plattform

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till Plattform med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringsbasanslutning med API:t för flödestjänst](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-lagringskällanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
