---
title: Experience Platform Launch Extensions
seo-title: Experience Platform Launch Extensions
description: Launch är nästa generation av tagghanteringsfunktioner från Adobe. Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
seo-description: Launch är nästa generation av tagghanteringsfunktioner från Adobe. Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 3%

---


# Experience Platform Launch-tillägg {#experience-platform-launch-extensions}

Experience Platform Launch är nästa generation av tagghanteringsfunktioner från Adobe. Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad funktion som ger mervärde.

En introduktion till funktionerna i Experience Platform Launch finns i resurserna nedan:
* Experience Platform Launch [dokumentation](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* Experience Platform Launch [snabbstartvideor](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Börja med [Introduktion till Översikt över](https://www.youtube.com/embed/rwqqkG1SERU) Experience Platform Launch [- och](https://helpx.adobe.com/analytics/how-to/adobe-launch-publishing-process.html)publiceringsprocessen och gå sedan vidare till nästa koncept.

## Hitta Launch-tilläggen i realtidsgränssnittet för CDP i Adobe {#how-to-find-extensions-in-interface}

Om du vill hitta Launch-tilläggen i CDP-gränssnittet i realtid i Adobe bläddrar du till **[!UICONTROL Destinations > Catalog]** och väljer **[!UICONTROL Extensions]** i **[!UICONTROL Types]** -filtret.

![Filtret Tillägg i gränssnittet](/help/rtcdp/destinations/assets/extensions-filter.png)

## Så här fungerar Launch-tillägg {#how-extensions-work}

Starta tillägg för att vidarebefordra råa händelsedata till flera olika typer av destinationer. Tänk på tillägg som en **typ av mål för vidarebefordran** av händelser. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är tillägget [](/help/rtcdp/destinations/gainsight-extension.md) Gainsight-anpassning eller [bekräftelsen från kundens tillägg](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

**Målen för profil-/segmentexport** i kunddata i Adobe i realtid hämtar Platform in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Exempel på sådana är [Amazon S3-molnlagringsdestinationen](/help/rtcdp/destinations/amazon-s3-destination.md) eller [Google Display &amp; Video 360-reklamdestinationen](/help/rtcdp/destinations/google-dv360-destination.md).

![Experience Platform Launch-tillägg jämfört med andra destinationer](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Fördelar med att använda Launch-tillägg {#extensions-benefits}

Experience Platform Launch är kostnadsfritt för befintliga Experience Cloud-kunder. Launch förenklar taggdistribution på din webbplats med lättanvända tillägg som du kan installera, konfigurera, uppdatera och ta bort. Launch är lite utrymmeskrävande på webbplatsen och gör att du kan behålla sidinläsningen snabbt.

>[!IMPORTANT]
>
>Du kan inte aktivera segment för att starta tillägg, men du kan konfigurera regler så att endast händelsedata vidarebefordras i vissa situationer. Läs mer nedan.

Du kan skapa *regler* som bestämmer när händelsedata ska vidarebefordras till tillägg. Denna kraftfulla funktion gör att du bara kan vidarebefordra händelsedata i vissa situationer, i motsats till att skicka händelsedata för varje interaktion. Mer information finns i reglerna i [startdokumentationen](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## Exempel på användningsexempel för Launch-tillägg {#extensions-use-cases}

Med Launch Extensions kan du tillgodose olika kundbehov. Exempel på användning av Launch-tillägg är:

* Du kan skicka webbplatsdata eller inbyggda appdata till Facebook via Facebooks pixeltillägg. Facebook Pixel anger vilka delar av din webbplats eller app en besökare navigerade till, vidarebefordrar den informationen till Facebook och du kan återannonsera besökaren via Facebook.
* Ni kan vidarebefordra händelsedata från era webbplatser och appar till Google Analytics för att analysera och fatta beslut baserat på dessa data.
* Du kan aktivera en chatbox-app på klientsidan vid rätt tidpunkt baserat på hur användarna interagerar med sidorna, enligt reglerna som du angav i Launch.


## Tilläggskategorier {#extension-categories}

Launch-tillägg kan delas in i följande kategorier i CDP i realtid i Adobe:

* [Reklam](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Datahantering Platform](/help/rtcdp/destinations/dmp-destinations.md)
* [E-postmarknadsföringsmål](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personanpassning](/help/rtcdp/destinations/personalization-destinations.md)
* [Undersökningar](/help/rtcdp/destinations/survey-destinations.md)
* [Kundens röst](/help/rtcdp/destinations/voice-of-customer-destinations.md)
