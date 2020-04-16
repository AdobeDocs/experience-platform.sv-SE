---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Google Ads-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc

---


# Skapa en Google Ads-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Google Ads-källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en Google Ads-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/payments.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till din Google Ads-kontoplattform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientCustomerId` | Kundens ID för annonskontot. |
| `developerToken` | Utvecklartoken som är associerad med hanterarkontot. |
| `refreshToken` | Uppdateringstoken som hämtats från Google för att auktorisera åtkomst till annonser. |
| `clientId` | Klient-ID för Google-programmet som används för att hämta uppdateringstoken. |
| `clientSecret` | Klienthemligheten för Google-programmet som används för att hämta uppdateringstoken. |

Mer information om hur du kommer igång finns i det här [Google Ads-dokumentet](https://developers.google.com/adwords/api/docs/guides/authentication).

## Anslut ditt Google Ads-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar ditt Google Ads-konto till Platform.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under kategorin *Advertising* väljer du **Google Ads** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/ads/catalog.png)

Sidan *Anslut till Google Ads* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du basanslutningen med ett namn, en valfri beskrivning och dina Google Ads-autentiseringsuppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för att upprätta den nya basanslutningen.

![koppla](../../../../images/tutorials/create/ads/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Google Ads-konto som du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ads/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt Google Ads-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta annonsdata till Platform](../../dataflow/advertising.md).