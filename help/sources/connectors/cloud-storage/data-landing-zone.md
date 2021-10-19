---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Källa för datallandningszon
topic-legacy: overview
description: Lär dig hur du ansluter Data Landing Zone till Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Du har tillgång till en [!DNL Data Landing Zone] behållare per sandlåda och den totala datavolymen för alla behållare begränsas till den totala datamängd som ingår i din licens för plattformsprodukter och -tjänster. Alla kunder med Platform och dess programtjänster som [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]och [!DNL Real-time Customer Data Platform] har etablerats med en [!DNL Data Landing Zone] behållare per sandlåda. Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] stöder SAS-baserad autentisering och dess data skyddas med standard [!DNL Azure Blob] Mekanismer för förvaringssäkerhet i vila och under transitering. SAS-baserad autentisering ger säker åtkomst till [!DNL Data Landing Zone] behållaren via en offentlig internetanslutning. Du behöver inte göra några nätverksändringar [!DNL Data Landing Zone] container, vilket betyder att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk. Plattformen har en strikt TTL-regel (time-to-live) på sju dagar för alla filer som överförs till en [!DNL Data Landing Zone] behållare. Alla filer tas bort efter sju dagar.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfiler eller -kataloger.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom kan vissa ASCII- eller Unicode-tecken, som kontrolltecken (som `0x00` till `0x1F`, `\u0081`och så vidare) tillåts inte heller. Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Data Landing Zone] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du hämtar data från [!DNL Data Landing Zone] behållare till Adobe Experience Platform med API:er eller användargränssnittet.

### Använda API:er

- [Skapa en [!DNL Data Landing Zone] källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Anslut [!DNL Data Landing Zone] till plattform med användargränssnittet](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
