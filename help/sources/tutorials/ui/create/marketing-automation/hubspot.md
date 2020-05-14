---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en HubSpot-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Skapa en HubSpot-källanslutning i användargränssnittet

> [!NOTE]
> HubSpot-anslutningen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en HubSpot-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en HubSpot-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/marketing-automation.md)för automatiserad marknadsföring.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt HubSpot-konto på plattformen måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `clientId` | Klient-ID som är associerat med ditt HubSpot-program. |
| `clientSecret` | Klienthemligheten som är kopplad till ditt HubSpot-program. |
| `accessToken` | Åtkomsttoken som fås när din OAuth-integration autentiseras initialt. |
| `refreshToken` | Den uppdateringstoken som erhölls när OAuth-integreringen autentiserades initialt. |

Mer information om hur du kommer igång finns i det här [HubSpot-dokumentet](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Anslut ditt HubSpot-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar ditt HubSpot-konto till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under kategorin *Marknadsföringsautomatisering* väljer du **HubSpot** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/hubspot/catalog.png)

Sidan *Anslut till HubSpot* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du basanslutningen med ett namn, en valfri beskrivning och dina HubSpot-uppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för att upprätta den nya basanslutningen.

![koppla](../../../../images/tutorials/create/hubspot/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det HubSpot-konto som du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/hubspot/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt HubSpot-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiseringssystemet för marknadsföring i Platform](../../dataflow/marketing-automation.md).