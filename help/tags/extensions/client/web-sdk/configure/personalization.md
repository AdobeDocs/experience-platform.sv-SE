---
title: Konfigurationsinställningar för Personalization
description: Konfigurera personaliseringsinställningar i Web SDK-taggtillägget.
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Konfigurationsinställningar för Personalization

I det här konfigurationsavsnittet kan du bestämma hur du vill dölja vissa delar av sidan när anpassat innehåll läses in. När inställningarna är korrekt konfigurerade ser du till att besökarna ser rätt personaliserat innehåll.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Personalization]**.

![Bild som visar personaliseringsinställningarna för SDK-taggtillägget för webben i användargränssnittet för taggar](../assets/web-sdk-ext-personalization.png)

Följande alternativ är tillgängliga:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Använd det här alternativet om du vill tillåta Web SDK att läsa och skriva de gamla `mbox`- och `mboxEdgeCluster`-cookies som används av `at.js` 1.x- eller 2.x-biblioteken. Med den här inställningen kan besökarprofiler bevaras intakta när du förflyttar dig mellan sidor med hjälp av Web SDK eller `at.js` på samma webbplats. Om du inte har `at.js` implementerat någonstans på webbplatsen behöver du inte aktivera den här kryssrutan. JavaScript-biblioteket som motsvarar kryssrutan är [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

## [!UICONTROL Prehiding style] {#prehiding-style}

Med den fördolda formatredigeraren kan du definiera anpassade CSS-regler för att dölja specifika avsnitt på en sida. När sidan har lästs in använder Web SDK den här stilen för att dölja de avsnitt som behöver personaliseras, hämtar personaliseringen och tar sedan bort de anpassade sidavsnitten. Med det här arbetsflödet kan besökare se personaliserat innehåll utan att behöva se hur personaliseringsprocessen läses in i eller flimrar. JavaScript-biblioteket som motsvarar denna kodredigerare är [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Det här avsnittet är inte en direkt konfigurationsinställning, utan en praktisk plats där du kan få implementeringskod. Implementera det här fördolda fragmentet i taggen `<head>` på din webbplats för att dölja det önskade innehållet medan Web SDK-biblioteket läses in.

>[!IMPORTANT]
>
>När du använder det fördolda fragmentet rekommenderar Adobe att du använder samma CSS-regel mellan det föregående och det föregående fragmentet.

## [!UICONTROL Enable personalization storage]

En kryssruta som gör att Web SDK kan lagra personaliseringshändelser. i webbläsarens lokala lager. Det är värdefullt när ni vill hålla reda på vilka upplevelser besökaren har sett över sidinläsningar.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

En nedrullningsbar meny som anger när Web SDK automatiskt hämtar klickningar på innehåll som returneras från Adobe Journey Optimizer.

* **[!UICONTROL Always]**: Samla in alla interaktioner med förslag.
* **[!UICONTROL Decorated elements only]**: Samla bara in interaktioner för element med attributen `data-aep-click-label` eller `data-aep-click-token` HTML.
* **[!UICONTROL Never]**: Samla inte in interaktioner med förslag.

JavaScript-biblioteket som motsvarar den här listrutan är [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Dess standardvärde är [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

En nedrullningsbar meny som anger när Web SDK automatiskt hämtar klickningar på innehåll som returneras från Adobe Target.

* **[!UICONTROL Always]**: Samla in alla interaktioner med förslag.
* **[!UICONTROL Decorated elements only]**: Samla bara in interaktioner för element med attributen `data-aep-click-label` eller `data-aep-click-token` HTML.
* **[!UICONTROL Never]**: Samla inte in interaktioner med förslag.

JavaScript-biblioteket som motsvarar den här listrutan är [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Dess standardvärde är [!UICONTROL Never].
