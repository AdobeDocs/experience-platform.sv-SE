---
keywords: Experience Platform;hem;populära ämnen;Google Cloud-lagring;Google cloud-lagring
solution: Experience Platform
title: Översikt över källanslutning för Google Cloud-lagring
topic-legacy: overview
description: Lär dig hur du ansluter Google Cloud-lagring till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Google Cloud Storage Connector

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure], så att du kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som JSON eller Parquet som är kompatibelt med Experience Data Model (XDM), eller i ett avgränsat format. Varje steg i processen är integrerat i källarbetsflödet. Med plattformen kan du hämta data från [!DNL Google Cloud Storage] via grupper.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Nödvändig konfiguration för att ansluta ditt [!DNL Google Cloud Storage]-konto

För att kunna ansluta till plattformen måste du först aktivera interoperabilitet för ditt [!DNL Google Cloud Storage]-konto. Om du vill komma åt interoperabilitetsinställningen öppnar du [!DNL Google Cloud Platform] och väljer **[!UICONTROL Settings]** från alternativet **[!UICONTROL Cloud Storage]** på navigeringspanelen.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Sidan **[!UICONTROL Settings]** visas. Här kan du se information om ditt [!DNL Google] projekt-ID och information om ditt [!DNL Google Cloud Storage]-konto. Välj **[!UICONTROL Interoperability]** i det övre huvudet för att få åtkomst till inställningarna för interoperabilitet.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Sidan **[!UICONTROL Interoperability]** innehåller information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt tjänstkonto. Välj **[!UICONTROL Create a Key for a Service Account]** om du vill generera ett nytt åtkomstnyckel-ID och en hemlig åtkomstnyckel för ditt tjänstkonto.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade ID för åtkomstnyckel och din hemliga åtkomstnyckel för att ansluta ditt [!DNL Google Cloud Storage]-konto till plattformen.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, även om de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Google Cloud Storage] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till plattformen med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringsbasanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-lagringskällanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
