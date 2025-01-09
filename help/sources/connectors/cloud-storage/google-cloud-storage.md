---
keywords: Experience Platform;hem;populära ämnen;Google Cloud Storage;Google cloud storage
solution: Experience Platform
title: Google Cloud Storage Source Connector - översikt
description: Lär dig hur du ansluter Google Cloud-lagring till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Google Cloud Storage Connector

>[!IMPORTANT]
>
>Du kan nu använda källan [!DNL Google Cloud Storage] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure], vilket gör att du kan hämta data från dessa system.

Lagringskällor i molnet kan hämta dina egna data till plattformen utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som JSON eller Parquet som är kompatibelt med Experience Data Model (XDM), eller i ett avgränsat format. Varje steg i processen är integrerat i källarbetsflödet. Med plattformen kan du hämta data från [!DNL Google Cloud Storage] via batchar.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förutsättningar för att ansluta ditt [!DNL Google Cloud Storage]-konto

För att kunna ansluta till plattformen måste du först aktivera interoperabilitet för ditt [!DNL Google Cloud Storage]-konto. Om du vill komma åt interoperabilitetsinställningen öppnar du [!DNL Google Cloud Platform] och väljer **[!UICONTROL Settings]** i alternativet **[!UICONTROL Cloud Storage]** på navigeringspanelen.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

Sidan **[!UICONTROL Settings]** visas. Här kan du se information om ditt projekt-ID för [!DNL Google] och information om ditt [!DNL Google Cloud Storage]-konto. Välj **[!UICONTROL Interoperability]** i det övre huvudet om du vill komma åt interoperabilitetsinställningarna.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

Sidan **[!UICONTROL Interoperability]** innehåller information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt tjänstkonto. Välj **[!UICONTROL Create a Key for a Service Account]** om du vill generera ett nytt åtkomstnyckel-ID och en hemlig åtkomstnyckel för ditt tjänstkonto.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Du kan använda ditt nyligen genererade åtkomstnyckel-ID och den hemliga åtkomstnyckeln för att ansluta ditt [!DNL Google Cloud Storage]-konto till plattformen.

Mer information finns i handboken om att [skapa och hantera tjänstkontonycklar](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) i [!DNL Google Cloud]-dokumentationen.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfilen eller -katalogen.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Den tas bort automatiskt om den anges.
- Följande reserverade URL-tecken måste ha escape-konverterats: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, men de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn tillåts inte: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (. .).

## Anslut [!DNL Google Cloud Storage] till plattformen

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Google Cloud Storage] till plattformen med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Google Cloud-lagringsbasanslutning med API:t för flödestjänst](../../tutorials/api/create/cloud-storage/google.md)
- [Utforska datastrukturen och innehållet i en molnlagringskälla med API:t för Flow Service](../../tutorials/api/explore/cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Skapa en Google Cloud-lagringskällanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
