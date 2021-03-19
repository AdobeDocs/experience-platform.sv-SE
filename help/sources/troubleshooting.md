---
keywords: Experience Platform;hem;populära ämnen;källor;problem;felsökning;felsökning av källor felsökning;källor faq;faq;source connectors;source connector;source connectors faqs;source connectors troubleshooting;
solution: Experience Platform
title: Felsökning av källor
topic: felsökning
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform källor.
translation-type: tm+mt
source-git-commit: 26e7116858574b366760ffd4f92b14117ccd28eb
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# (Beta) Felsökningsguide för källor

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform källor. Om du har frågor och felsökning som rör andra [!DNL Platform]-tjänster, inklusive de som påträffas i alla [!DNL Platform] API:er, kan du läsa [felsökningsguiden för Experience Platform](../landing/troubleshooting.md).

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
- Ogiltiga URL-sökvägstecken tillåts inte. Kodpunkter som `\uE000` är inte giltiga Unicode-tecken, även om de är giltiga i NTFS-filnamn. Dessutom tillåts inte vissa ASCII- eller Unicode-tecken, som kontrolltecken (0x00 till 0x1F, \u0081 osv.). Regler som styr Unicode-strängar i HTTP/1.1 finns i [RFC 2616, avsnitt 2.2: Grundregler](https://www.ietf.org/rfc/rfc2616.txt) och [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Följande filnamn är inte tillåtna: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punkttecken (.) och två punkttecken (.).
- Det maximala antalet filer per grupp är 1 500, med en maximal batchstorlek på 100 GB.
- Det högsta antalet egenskaper eller fält per rad är 10 000.
- Det högsta antalet batchar som kan skickas per användare, per minut, är 138.

### Vilka datatyper stöds?

Datatyper som stöds är heltal, strängar, booleska värden, datetime-objekt, arrayer och objekt.

### Vilka datum- och tidsformat stöds?

Källor har stöd för en mängd olika datetime-format när data hämtas. Mer information om vilka datetime-format som stöds finns i [funktionsguiden för dataprep](../data-prep/dates.md).

### Hur formaterar jag arrayer i CSV-, JSON- och Parquet-filer?

JSON- och Parquet-filer har inbyggt stöd för arrayer. För platta strukturer, som CSV-filer, stöds inte arrayer. Strängar med flera värden kan emellertid delas upp i en array med hjälp av förinställningsfunktioner för data, som explodera och förena. Mer information om dessa förinställningsfunktioner finns i [handboken för förinställningsfunktioner för data](../data-prep/functions.md#string)

### Vilka källor stöder partiellt intag?

Alla källor för batchförtäring stöder partiellt intag. Källor för direktuppspelning stöder dock inte partiellt intag.

### När ska jag använda partiellt intag?

Delvis intag bör användas om du inte har **begränsningar för**, som att hela filen hämtas till Platform. Alternativt kan man använda en del av intaget om man inte har något emot att få in data som kan innehålla fel.

### Vilket är det typiska feltröskelvärdet för partiellt intag?

Det finns inget &quot;typiskt feltröskelvärde&quot; för partiellt intag. I stället kan det här värdet variera från fall till fall. Som standard är feltröskelvärdet 5 %.