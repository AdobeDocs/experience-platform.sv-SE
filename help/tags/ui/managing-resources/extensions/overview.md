---
title: Tillägg
description: Lär dig hur taggtillägg fungerar i Adobe Experience Platform.
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
source-git-commit: 31811b7448a285ee5d25872641354a6981c64471
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Tillägg

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Ett tillägg är en paketerad koduppsättning som utökar funktionerna som anges i taggar eller vidarebefordran av händelser.

När du lägger till ett tillägg läggs nya dataelement och nya alternativ till för att skapa regler.

Tillägg avgör vilka element som är tillgängliga när du skapar egenskaper, regler och dataelement. De innehåller följande:

* Händelser, villkor och undantag
* Dataelement
* Kod på klientsidan

Använd länkarna högst upp i listan Tillägg om du vill visa installerade tillägg, katalogen för tillägg eller uppdateringar.

Välj ett tillägg och välj sedan [!UICONTROL Configure] om du vill visa och ändra tilläggets inställningar. Mer information finns i avsnittet om [lägga till ett nytt tillägg](#add-a-new-extension) om du vill ha information om tilläggsalternativ.

>[!IMPORTANT]
>
>Ändringarna börjar inte gälla förrän de är [publicerad](../../publishing/overview.md).

Som standard har Adobe tillägg som stöder vanliga integreringar. Tillägg kan ändras med anpassade konfigurationer. Konfigurationer tillhandahålls via tilläggen. Om du vill skapa en konfiguration markerar du tilläggskortet och väljer sedan **[!UICONTROL Add New Configuration]**.

## Tilläggskatalog

Använd tilläggskatalogen för att söka, konfigurera och driftsätta marknadsförings- och annonseringsteknik som byggts och underhålls av oberoende programvaruleverantörer samt tillägg för lösningar från Adobe.

Sidan Tillägg innehåller tre vyer:

* Installerad

  Visar alla installerade tillägg.

* Katalog
* Visar alla tillgängliga tillägg
* Uppdateringar

  Visar uppdateringar av installerade tillägg.

Välj **[!UICONTROL Extensions]** för att se alla installerade tillägg. Du kan också använda katalogen för att visa en lista över alla tillgängliga tillägg och vilka tillägg som har tillgängliga uppdateringar.

Se [Referens för tillägg](../../../extensions/client/overview.md) om du vill ha information om tillägg som ägs av Adobe.

## Lägg till ett nytt tillägg {#add-a-new-extension}

Taggar är mycket utökningsbara. Tillägg lägger till kärnfunktioner i taggar. Ett vanligt användningsområde för tillägg är att skapa integreringar med andra program.

>[!TIP]
>
>Använd hjälpen för produkten i den högra panelen för att lära dig mer om tillägg och visa ytterligare tillgängliga resurser.

1. Från en egenskaps översiktssida öppnar du **[!UICONTROL Extensions]** -fliken.
1. Välj ett tillägg.

   ![Fliken Katalog med huvudtillägg på fliken Tillägg.](../../../images/extensions.png)

   * Om tillägget finns väljer du det i tilläggskatalogen.
   * För musen över ett tillägg i listan för att konfigurera eller inaktivera det.
   * Lägg till andra tillägg från katalogen om de inte finns med i listan.

   Core-tillägget är startpunkten för ditt nya tillägg. Standardtillägget innehåller:

   * Standardhändelse
   * Standardvillkor och undantag
   * Standardkod på klientsidan

   Dessa standardinställningar är grunden för de anpassade regler som du skapar för att skapa tillägget.

När du skapar eller redigerar element kan du spara och bygga på [aktivt bibliotek](../../publishing/libraries.md#active-library). Ändringen sparas omedelbart i biblioteket och en bygge körs. Byggets status visas. Du kan också skapa ett nytt bibliotek från listrutan Aktiva bibliotek.

## Konfigurera ett tillägg

Musknapp över ett installerat tillägg och välj **[!UICONTROL Configure]**.

>[!NOTE]
>
>Vissa tillägg kräver ingen konfiguration och har inga konfigurationsalternativ.

Varje konfigurerbart tillägg har unika alternativ. Se [Referens för tillägg](../../../extensions/client/overview.md) om du vill ha information om vilka alternativ som är tillgängliga för varje tillägg i Adobe.
