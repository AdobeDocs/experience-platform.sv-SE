---
keywords: Experience Platform;hem;populära ämnen;källor;problem;felsökning;felsökning av källor felsökning;källor faq;faq;source connectors;source connector;source connectors faqs;source connectors troubleshooting;
solution: Experience Platform
title: Felsökning av källor
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform källor.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Felsökningsguide för källor

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform källor. För frågor och felsökning relaterade till andra [!DNL Platform] tjänster, inklusive sådana som påträffas i alla [!DNL Platform] API:er, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

## Frågor och svar

Nedan följer en lista med svar på vanliga frågor om källor.

### Måste jag ändra inställningarna för nätverkssäkerhet för att kunna aktivera källor?

Du kan behöva tillåtslista vissa IP-adresser för att kunna aktivera källor. Mer information finns i dokumentationen för din specifika källanslutning.

### Vilka autentiseringstyper stöds av källor?

Källor kan autentiseras med hjälp av anslutningssträngar, användarnamn och lösenord, eller via token och nycklar. Specifik information om vilka autentiseringstyper som stöds finns i dokumentationen för den angivna källkopplingen.

### Varför misslyckas alla mina senaste flöden?

Om du märker att alla dina senaste körningar misslyckas kan dina autentiseringsuppgifter ha ändrats eller gått ut. Försök att åtgärda problemet genom att uppdatera anslutningen med de senaste autentiseringsuppgifterna.

### Vilka filtyper stöds?

De filtyper som stöds för närvarande är avgränsade filer, JSON och Parquet.

### Vilka begränsningar gäller för filnamn och filstorlekar?

Här följer en lista med begränsningar som du måste ta hänsyn till för filer i källor.

- Katalog- och filkomponentnamn får inte innehålla fler än 255 tecken.
- Katalog- och filnamn får inte sluta med ett snedstreck (`/`). Om det finns kommer det att tas bort automatiskt.
- Följande reserverade URL-tecken måste escape-konverteras: `! ' ( ) ; @ & = + $ , % # [ ]`
- Följande tecken tillåts inte: `" \ / : | < > * ?`.
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000`, som är giltigt i NTFS-filnamn, är inte giltiga Unicode-tecken. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Information om regler för Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).
- Det maximala antalet filer per grupp är 1 500, med en maximal batchstorlek på 100 GB.
- Det högsta antalet egenskaper eller fält per rad är 10 000.
- Det högsta antalet batchar som kan skickas per användare, per minut, är 138.

### Vilka datatyper stöds?

Datatyper som stöds är heltal, strängar, booleska värden, datetime-objekt, arrayer och objekt.

### Vilka datum- och tidsformat stöds?

Källor har stöd för en mängd olika datetime-format när data hämtas. Mer information om vilka datetime-format som stöds finns i datumavsnittet i [guide för hantering av dataformat](../data-prep/data-handling.md#dates) i Data Prep-dokumentationen.

### Hur formaterar jag arrayer i CSV-, JSON- och Parquet-filer?

JSON- och Parquet-filer har inbyggt stöd för arrayer. För platta strukturer, som CSV-filer, stöds inte arrayer. Strängar med flera värden kan emellertid delas upp i en array med hjälp av förinställningsfunktioner för data, som explodera och förena. Mer information om dessa förinställningsfunktioner finns i [guide för preflight-funktioner](../data-prep/functions.md#string)

### Vilka källor stöder partiellt intag?

Alla källor för batchförtäring stöder partiellt intag. Källor för direktuppspelning stöder dock inte partiellt intag.

### När ska jag använda partiellt intag?

Delvis intag bör användas om du **not** har begränsningar, t.ex. att hela filen hämtas till Platform. Alternativt kan man använda en del av intaget om man inte har något emot att få in data som kan innehålla fel.

### Vilket är det typiska feltröskelvärdet för partiellt intag?

Det finns inget &quot;typiskt feltröskelvärde&quot; för partiellt intag. I stället kan det här värdet variera från fall till fall. Som standard är feltröskelvärdet 5 %.

### Hur lång tid tar det att uppdatera flödeskörningsstatus efter att ett nytt dataflöde har skapats?

Flödeskörningar genereras inte omedelbart och kan ta mellan två och tre minuter att uppdatera efter att de har angetts `startTime`. Om du kontrollerar status för en flödeskörning returneras ingen information om flödeskörningen omedelbart efter att ett nytt dataflöde har skapats `lastRunDetails` eftersom det ännu inte har hänt. Vi rekommenderar att du tillåter att dataflödet genereras några minuter innan du kontrollerar status för flödeskörningen.