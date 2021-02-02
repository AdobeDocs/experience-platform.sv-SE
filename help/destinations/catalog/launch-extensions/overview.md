---
keywords: starta tillägg;starta tillägg;startmål; plattformsstarttillägg;plattformsstarttillägg;plattformsstartmål
title: Experience Platform Launch Extensions
seo-title: Experience Platform Launch Extensions
description: Launch är nästa generation av tagghanteringsfunktioner från Adobe. Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
seo-description: Launch är nästa generation av tagghanteringsfunktioner från Adobe. Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Adobe Experience Platform Launch-tillägg {#overview.md}

Adobe Experience Platform Launch är nästa generation av tagghanteringsfunktioner från Adobe. Platform Launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Platform Launch erbjuds Adobe Experience Cloud-kunder som en inkluderad, värdeskapande funktion.

En introduktion till funktionerna i Experience Platform Launch finns i resurserna nedan:
- Adobe Experience Platform Launch [dokumentation](https://experienceleague.adobe.com/docs/launch/using/overview.html)
- Adobe Experience Platform Launch [snabbstartsvideor](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Börja med [Introduktion till Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) och [Översikt över publiceringsprocessen](https://helpx.adobe.com/analytics/how-to/adobe-launch-publishing-process.html) och gå sedan vidare till nästa koncept.

## Hitta plattformsstartstilläggen i plattformsgränssnittet {#how-to-find-extensions-in-interface}

Om du vill hitta plattformsstartstilläggen i plattformsgränssnittet går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** och väljer **[!UICONTROL Extensions]** i **[!UICONTROL Types]**-filtret.

![Filtret Tillägg i gränssnittet](../../assets/catalog/launch-extensions/filter.png)

## Så här fungerar tillägg för plattformsstart {#how-extensions-work}

Plattformsstartstillägg vidarebefordrar råa händelsedata till flera typer av destinationer. Tänk på tillägg som en **typ av händelsespårning**-typ av mål. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är [tillägget för Gainsight-anpassning](../personalization/gainsight.md) eller [Bekräfta röst för kundtillägget](../voice/confirmit-digital-feedback.md).

**Profil-/** segmentexportdestinationer i Adobe Experience Platform samlar in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Exempel på sådana är [Amazon S3-molnlagringsmålet](../cloud-storage/amazon-s3.md) eller [Google Display &amp; Video 360-annonsmålet](../advertising/google-dv360.md).

![Experience Platform Launch-tillägg jämfört med andra destinationer](../../assets/common/launch-and-other-destinations.png)

## Fördelar med att använda plattformsstartstillägg {#extensions-benefits}

Adobe Experience Platform Launch är kostnadsfritt för befintliga Experience Cloud-kunder. Platform Launch förenklar taggdistribution på din webbplats med lättanvända tillägg som du kan installera, konfigurera, uppdatera och ta bort. Platform Launch har ett litet utrymme på din webbplats och gör att du kan behålla sidinläsningen snabbt.

>[!IMPORTANT]
>
>Du kan inte aktivera segment för plattformsstartstillägg, men du kan konfigurera regler så att endast händelsedata vidarebefordras i vissa situationer. Läs mer nedan.

Du kan skapa *regler* som bestämmer när händelsedata ska vidarebefordras till tillägg. Denna kraftfulla funktion gör att du bara kan vidarebefordra händelsedata i vissa situationer, i motsats till att skicka händelsedata för varje interaktion. Mer information finns i [Adobe Experience Platform Launch-dokumentationen](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Exempel på användningsexempel för plattformsstartstillägg {#extensions-use-cases}

Med plattformsstartstillägg kan du tillgodose olika kundbehov. Exempel på användning av plattformstillägg är:

- Du kan skicka webbplatsdata eller inbyggda appdata till Facebook via Facebooks pixeltillägg. Facebook Pixel anger vilka delar av din webbplats eller app en besökare navigerade till, vidarebefordrar den informationen till Facebook och du kan återannonsera besökaren via Facebook.
- Ni kan vidarebefordra händelsedata från era webbplatser och appar till Google Analytics för att analysera och fatta beslut baserat på dessa data.
- Du kan aktivera en chatbox-app på klientsidan vid rätt tidpunkt baserat på hur dina användare interagerar med dina sidor, enligt reglerna som du angav i Platform Launch.

## Tilläggskategorier {#extension-categories}

Plattformsstartstillägg kan delas in i följande kategorier i Plattform:

- [Reklam](../advertising/overview.md)
- [Analytics](../analytics/overview.md) 
- [Datahanteringsplattform](../data-management/overview.md)
- [E-postmarknadsföringsmål](../email-marketing/overview.md)
- [Personanpassning](../personalization/overview.md)
- [Undersökningar](../survey/overview.md)
- [Kundens röst](../voice/overview.md)
