---
title: Skapa en Exchange-lista för ett tillägg
description: Lär dig hur du lägger till tillägget i den offentliga katalogen i Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Skapa en utbyteslista för ett tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Adobe Experience Platform har en enda enhetlig katalog där användarna kan visa taggtillägg som är tillgängliga för installation. Katalogen är tillgänglig i produkten och innehåller tillägg av tre typer:

1. **Offentliga tillägg**: Dessa är kompletta tillägg som är utformade för att användas av alla användare i produktionen.
1. **Privata tillägg**: Dessa är färdiga tillägg som tagits fram för produktion, men har utvecklats av andra användare i företaget och är endast tillgängliga för användare i ditt företag.
1. **Utvecklingstillägg**: Dessa tillägg är under aktiv utveckling och är endast tillgängliga inom företaget och endast på en egenskap som specifikt har angetts som en Development-egenskap.

Förutom tilläggen i produktkatalogen har offentliga tillägg även listor i [Experience Cloud Exchange App Marketplace](https://exchange.adobe.com/apps/browse/ec).

Med dessa listor kan tilläggsutvecklare publicera funktionsbeskrivningar, tillhandahålla länkar till ytterligare support och dokumentation samt marknadstillägg till potentiella användare som kanske inte känner till ditt företag eller funktionaliteten i ditt tillägg. På den här marknadsplatsen har tillägget en offentlig lista som kan visas utan att användaren autentiseras för Platform. För offentliga tillägg är det ett obligatoriskt steg att skapa den här Exchange-listan.

>[!TIP]
>
>När din Exchange-lista publiceras läggs en länk automatiskt till listinnehållet så att dina kunder och potentiella kunder kan klicka och `Connect with publisher` för mer information om produkter och tjänster. Din e-postadress för kontakt visas inte eftersom de här meddelandena vidarebefordras till dig via Exchange-systemet.

Om du inte har något företag att ladda upp och testa tilläggspaketet bör du registrera dig för Exchange-programmet och börja en lista. Detta kommer att utlösa skapandet av ett företagskonto (det tar en stund, du får ett e-postmeddelande när det är klart) som du kan använda för att överföra och testa tillägget. Även här krävs Exchange-listor bara för offentliga tillägg.

Om du redan har ett företagskonto, eller om du inte behöver en Exchange-lista (endast privata tillägg), kan du hoppa över resten av det här steget och fortsätta till [ladda upp och testa tillägget](./upload-and-test.md).

## Skapa en lista

>[!NOTE]
>
>Följande process beskriver hur du skapar en programlista i programmet Adobe Exchange. Detta är den term som används för de olika integreringarna och tilläggen i Adobe Experience Platform.

![Experience Cloud App Manager-länkplats](../images/getting-started/app-mgr-link.png)

1. Logga in på [Exchange Partner-webbplats](https://partners.adobe.com/exchangeprogram/experiencecloud). När du är inloggad väljer du **App Manager** länk bredvid ditt namn.
1. Välj **Skapa nytt program** och sedan välja **Skapa ny app** för en anpassad lösning, eller välj en lämplig mall.
1. Ange din listinformation. Mer information om App Manager finns i den fullständiga [artikel](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). Listinformation bör vara mycket tydlig med vad tillägget gör och varför det är användbart. Listan fungerar som ett marknadsföringsutrymme för din app. Befordra tillägget här med tydliga beskrivningar, länkar till landningssidor på webbplatsen, länkar till hjälpdokument eller e-postadresser till support osv. Även om utrymmet i tilläggsvyn är begränsat, ger Exchange-listan möjlighet att marknadsföra både ditt tillägg och ditt företag. Nedan följer förslag på hur du kan förbättra erbjudandet om tillägg:
   - **Appikon** - Kontrollera att ikonen för Exchange-listan har rätt dimensioner, 512 x 512 för png eller 1:1 för jpg.

      >[!NOTE]
      >
      >Detta är ett annat filformat än det som används i tilläggskoden. Tillägget i sig innehåller en svg-fil som [icon](../manifest.md).

   - **Aktuell bild** - Få uppmärksamhet genom att använda en bild som kan vara fristående och som visar ert varumärke och framhäver er applikation. Den bild som visas när någon delar en länk till din Exchange-lista eller publicerar om den på sociala medier. Det måste därför vara en modellbeteckning för ert varumärke.
   - **App Publisher&#39;s Logo** - Det här är din företagslogotyp, kontrollera att ikonen har rätt dimensioner på 1 280 x 720 eller 2 560 x 1 440 (16:9) i png- eller jpg-format.
   - **Konfigurationsanvisningar** - Informera kunderna om hur de konfigurerar ditt Adobe Experience Platform-tillägg. Försäkra dig om att de förstår de inställningar som krävs och nästa steg när [konfigurationsvy](../configuration.md) visas omedelbart efter installation av tillägget i en egenskap.
   - **Taggar** - På den första sidan där du redigerar din lista ska du lägga till ordet&quot;Starta&quot; i fältet&quot;Anpassade taggar&quot;. Detta gör att din lista visas i sökningar efter taggar på Exchange Marketplace:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandlådor** - Du har tillgång till Adobe Solutions via ett sandlådekonto där du har tillgång till en fullt fungerande version av Adobe Experience Platform. Dessa sandlådekonton begärs när du skapar programlistan. I **Anslutningar** markerar du de specifika anslutningar som gäller för det program du skapade (ditt taggtillägg) och när du klickar på **Spara** genereras sandlådebegäran om det behövs.
1. Skicka din lista. Adobe Exchange-teamet granskar din ansökan och ger feedback om det behövs uppdateringar. Om du markerar **publicera omedelbart** när du skickar in din lista kommer den att publiceras omedelbart efter godkännande. Om du vill publicera programmet vid ett senare tillfälle låter du kryssrutan vara avmarkerad. När tilläggslistan är godkänd visas en blå **Publicera** visas bredvid den på programlistans (tilläggets) listsida.

### Skapa en effektiv lista

Ta en titt på [Riktlinje för programinlämning](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) för detaljerad information om hur du skapar den mest engagerande listan.

#### När du har skickat in Exchange-listan

När ansökan har skickats in kommer Adobe Exchange-teamet att granska den och antingen godkänna den eller svara med kommentarer om ändringarna. Den här processen beskrivs i riktlinjerna för att skicka appar.

Om du inte har någon inloggning på Exchange-webbplatsen kontrollerar du att din e-postadress är registrerad för Exchange-programmet genom att följa instruktionerna i [Programregistreringsguide](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Varje användare måste associera sin e-post med partnerkontot för sitt företag. Frågor om den här processen kan dirigeras via e-post till <ExchangeHelpEC@adobe.com>.

#### Uppdatera Exchange-listan efter första godkännande

När du uppdaterar tillägget, eller bara behöver uppdatera Exchange-listan, loggar du in på [Partnerportal](https://partners.adobe.com/exchangeprogram/experiencecloud)och välj knappen App Manager bredvid ditt namn. Välj sedan programmet och följ det flöde ovan som användes för att skapa listan. När Adobe Exchange-teamet har skickats in på nytt kommer de att granska ändringarna och antingen godkänna ändringarna eller svara med kommentarer om ändringarna.

## Länka tilläggspaketet till din lista

När din lista har godkänts och är allmänt tillgänglig rekommenderar vi att du tillhandahåller en länk till den offentliga förteckningen i `exchange_url` fält för `extension.json` i tilläggspaketet.  Då skapas länken &quot;Mer information&quot; i taggtilläggskatalogen så att användare i produkten kan hitta din lista och den extra informationen.
