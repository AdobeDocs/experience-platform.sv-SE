---
title: Skapa en Exchange-lista för ett tillägg
description: Lär dig hur du lägger till tillägget i den offentliga katalogen i Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 3%

---

# Skapa en utbyteslista för ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Adobe Experience Platform har en enda enhetlig katalog där användarna kan visa taggtillägg som är tillgängliga för installation. Katalogen är tillgänglig i produkten och innehåller tillägg av tre typer:

1. **Offentliga tillägg**: De här är slutförda tillägg som är utformade för att användas i produktion av alla användare.
1. **Privata tillägg**: De här är slutförda tillägg som är utformade för produktion, men har utvecklats av andra användare i ditt företag och är bara tillgängliga för användare i ditt företag.
1. **Utvecklingstillägg**: De här tilläggen är under aktiv utveckling och är bara tillgängliga inom ditt företag och endast på en egenskap som är specifikt angiven som en Development-egenskap.

Publika tillägg skiljer sig från tilläggen i produktkatalogen och det finns även listor i [Experience Cloud Exchange App Marketplace](https://exchange.adobe.com/apps/browse/ec).

Med dessa listor kan tilläggsutvecklare publicera funktionsbeskrivningar, tillhandahålla länkar till ytterligare support och dokumentation samt marknadstillägg till potentiella användare som kanske inte känner till ditt företag eller funktionaliteten i ditt tillägg. På den här marknadsplatsen har tillägget en offentlig lista som kan visas utan att användaren autentiseras för Experience Platform. För offentliga tillägg är det ett obligatoriskt steg att skapa den här Exchange-listan.

>[!TIP]
>
>När din Exchange-lista publiceras läggs en länk automatiskt till listinnehållet som gör att dina kunder och potentiella kunder kan klicka och `Connect with publisher` om du vill ha mer information om dina produkter och tjänster. Din e-postadress för kontakt visas inte eftersom de här meddelandena vidarebefordras till dig via Exchange-systemet.

Om du inte har något företag att ladda upp och testa tilläggspaketet bör du registrera dig för Exchange-programmet och börja en lista. Detta kommer att utlösa skapandet av ett företagskonto (det tar en stund, du får ett e-postmeddelande när det är klart) som du kan använda för att överföra och testa tillägget. Även här krävs Exchange-listor bara för offentliga tillägg.

Om du redan har ett företagskonto, eller om du inte behöver en Exchange-lista (endast privata tillägg), kan du hoppa över resten av det här steget och fortsätta med att [överföra och testa tillägget](./upload-and-test.md).

## Skapa en lista

>[!NOTE]
>
>Följande process beskriver hur du skapar en programlista i Adobe Exchange-programmet. Detta är den term som används för de olika integreringarna och tilläggen i Adobe Experience Platform.

![Experience Cloud App Manager-länkplats](../images/getting-started/app-mgr-link.png)

1. Logga in på [Exchange Partner-webbplatsen](https://partners.adobe.com/exchangeprogram/experiencecloud). När du är inloggad väljer du länken **App Manager** bredvid ditt namn.
1. Välj fliken **Skapa nytt program** och välj sedan **Skapa ny app** för en anpassad lösning, eller välj en lämplig mall.
1. Ange din listinformation. Mer information om App Manager finns i den fullständiga [artikeln](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). Listinformation bör vara mycket tydlig med vad tillägget gör och varför det är användbart. Listan fungerar som ett marknadsföringsutrymme för din app. Befordra tillägget här med tydliga beskrivningar, länkar till landningssidor på webbplatsen, länkar till hjälpdokument eller e-postadresser till support osv. Även om utrymmet i tilläggsvyn är begränsat, ger Exchange-listan möjlighet att marknadsföra både ditt tillägg och ditt företag. Nedan följer förslag på hur du kan förbättra erbjudandet om tillägg:
   - **Programikon** - Kontrollera att ikonen för Exchange-listan har rätt dimensioner, 512 x 512 för png eller 1:1-proportioner för jpg.

     >[!NOTE]
     >
     >Detta är ett annat filformat än det som används i tilläggskoden. Tillägget i sig innehåller en SVG-fil som [ikon](../manifest.md).

   - **Aktuell bild** - Få uppmärksamhet genom att använda en bild som kan vara fristående och visa ditt varumärke och framhäva ditt program. Den bild som visas när någon delar en länk till din Exchange-lista eller publicerar om den på sociala medier. Det måste därför vara en modellbeteckning för ert varumärke.
   - **Programutgivarens logotyp** - Det här är företagets logotyp, kontrollera att ikonen har rätt dimensioner på 1 280 x 720 eller 2 560 x 1 440 (16:9) i png- eller jpg-format.
   - **Konfigurationsanvisningar** - Informera kunder om hur du konfigurerar ditt Adobe Experience Platform-tillägg. Kontrollera att de förstår alla nödvändiga inställningar och nästa steg när [konfigurationsvyn](../configuration.md) visas omedelbart efter att du har installerat tillägget i en egenskap.
   - **Taggar** - På den första sidan där du redigerar din lista måste du ta med ordet&quot;Starta&quot; i fältet&quot;Anpassade taggar&quot;. Detta gör att din lista visas i sökningar efter taggar på Exchange Marketplace:

     ![](../images/getting-started/custom-tags.jpg)
   - **Sandlådor** - Din åtkomst till Adobe Solutions sker via ett sandlådekonto där du har tillgång till en fullt fungerande version av Adobe Experience Platform. Dessa sandlådekonton begärs när du skapar programlistan. I avsnittet **Anslutningar** markerar du de specifika anslutningar som gäller för det program du skapade (ditt taggtillägg). När du klickar på **Spara** genereras sandlådebegäran om det behövs.
1. Skicka din lista. Adobe Exchange-teamet granskar din ansökan och ger feedback om det behövs uppdateringar. Om du markerar kryssrutan **publicera omedelbart** när du skickar din lista publiceras den direkt när den har godkänts. Om du vill publicera programmet vid ett senare tillfälle låter du kryssrutan vara avmarkerad. När din tilläggslista har godkänts visas en blå **Publicera**-knapp bredvid den på programlistsidan (tilläggssidan).

### Skapa en effektiv lista

Ta en titt på [riktlinjerna för programinlämning](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) för mer information om hur du skapar den mest engagerande listan.

#### När du har skickat in Exchange-listan

När ansökan har skickats in kommer Adobe Exchange-teamet att granska den och antingen godkänna den eller svara med kommentarer om ändringarna. Den här processen beskrivs i riktlinjerna för att skicka appar.

Om du inte har loggat in på Exchange-webbplatsen kontrollerar du att din e-postadress är registrerad för Exchange-programmet genom att följa instruktionerna i [programregistreringsguiden](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Varje användare måste associera sin e-post med partnerkontot för sitt företag. Frågor om den här processen kan dirigeras via e-post till <ExchangeHelpEC@adobe.com>.

#### Uppdatera Exchange-listan efter första godkännande

När du uppdaterar tillägget, eller bara behöver uppdatera Exchange-listan, loggar du in på [partnerportalen](https://partners.adobe.com/exchangeprogram/experiencecloud) och väljer knappen App Manager bredvid ditt namn. Välj sedan programmet och följ det flöde ovan som användes för att skapa listan. När Adobe Exchange-teamet har skickat in det på nytt kommer de att granska ändringarna och antingen godkänna ändringarna eller svara med kommentarer om ändringarna.

## Länka tilläggspaketet till din lista

När din lista har godkänts och är allmänt tillgänglig rekommenderar vi att du tillhandahåller en länk till den offentliga listan i fältet `exchange_url` för filen `extension.json` i tilläggspaketet.  Då skapas länken &quot;Mer information&quot; i taggtilläggskatalogen så att användare i produkten kan hitta din lista och den extra informationen.
