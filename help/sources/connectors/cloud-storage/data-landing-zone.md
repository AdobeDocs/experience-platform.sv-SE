---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Källa för datallandningszon
topic-legacy: overview
description: Lär dig hur du ansluter Data Landing Zone till Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] är ett  [!DNL Azure Blob] lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för import och utgång av filer i och från plattformen via källor och mål. Du har åtkomst till en [!DNL Data Landing Zone]-behållare per sandlåda, och den totala datavolymen för alla behållare är begränsad till den totala datamängd som följer med din licens för plattformsprodukter och tjänster. Alla kunder med Platform och dess programtjänster som [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] och [!DNL Real-time Customer Data Platform] har etablerats med en [!DNL Data Landing Zone]-behållare per sandlåda. Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] stöder SAS-baserad autentisering och dess data skyddas med  [!DNL Azure Blob] standardmekanismer för lagringssäkerhet vid vila och överföring. SAS-baserad autentisering gör att du på ett säkert sätt kan komma åt din [!DNL Data Landing Zone]-behållare via en offentlig internetanslutning. Du behöver inte göra några nätverksändringar för att komma åt din [!DNL Data Landing Zone]-behållare, vilket innebär att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk. Plattformen tillämpar en strikt TTL (time-to-live) på sju dagar för alla filer som överförs till en [!DNL Data Landing Zone]-behållare. Alla filer tas bort efter sju dagar.

## Namnbegränsningar för filer och kataloger

Nedan följer en lista över begränsningar som du måste ta hänsyn till när du namnger molnlagringsfiler eller -kataloger.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, även om de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, t.ex. kontrolltecken (t.ex. `0x00` till `0x1F`, `\u0081`). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).

## Anslut [!DNL Data Landing Zone] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du överför data från din [!DNL Data Landing Zone]-behållare till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.

### Använda API:er

- [Skapa en  [!DNL Data Landing Zone] källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringskälla med API:t för Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Använda gränssnittet

- [Anslut [!DNL Data Landing Zone] till plattformen med användargränssnittet](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Skapa ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/batch/cloud-storage.md)
