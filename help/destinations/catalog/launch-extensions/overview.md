---
keywords: starta tillägg;starta tillägg;startmål; platform launch extensions;platform launch extension;platform launch destination
title: Adobe Experience Platform Launch-tillägg
description: Adobe Experience Platform Launch är nästa generation av tagghanteringsfunktioner från Adobe. platform launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Adobe Experience Platform Launch-tillägg

Adobe Experience Platform Launch är nästa generation av tagghanteringsfunktioner från Adobe. platform launch ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. platform launch erbjuds Adobe Experience Cloud-kunder som en inkluderad funktion som ger mervärde.

En introduktion till funktionerna i Experience Platform Launch finns i resurserna nedan:

- Adobe Experience Platform Launch [dokumentation](https://experienceleague.adobe.com/docs/launch/using/home.html)
- Adobe Experience Platform Launch [snabbstartsvideor](../../../tags/quick-start/videos.md). Börja med [Introduktion till Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) och [Översikt över publiceringsprocessen](https://helpx.adobe.com/analytics/how-to/adobe-launch-publishing-process.html) och gå sedan vidare till nästa koncept.

## Hitta Platforma launcherna i plattformsgränssnittet {#how-to-find-extensions-in-interface}

Om du vill hitta programtilläggen i plattformsgränssnittet går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** och väljer **[!UICONTROL Extensions]** i filtret **[!UICONTROL Types]**.

![Filtret Tillägg i gränssnittet](../../assets/catalog/launch-extensions/filter.png)

## Så här fungerar tillägg i Platforma launcher {#how-extensions-work}

platform launch-tillägg vidarebefordrar råa händelsedata till flera typer av destinationer. Tänk på tillägg som en **typ av händelsespårning**-typ av mål. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är [tillägget för Gainsight-anpassning](../personalization/gainsight.md) eller [Bekräfta röst för kundtillägget](../voice/confirmit-digital-feedback.md).

**Profil-/** segmentexportdestinationer i Adobe Experience Platform samlar in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Exempel på sådana är [Amazon S3-molnlagringsmålet](../cloud-storage/amazon-s3.md) eller [Google Display &amp; Video 360-annonsmålet](../advertising/google-dv360.md).

![Experience Platform Launch-tillägg jämfört med andra destinationer](../../assets/common/launch-and-other-destinations.png)

## Fördelar med att använda tillägg för Platforma launcher {#extensions-benefits}

Adobe Experience Platform Launch är kostnadsfritt för befintliga Experience Cloud-kunder. platform launch förenklar taggdistribution på din webbplats med lättanvända tillägg som du kan installera, konfigurera, uppdatera och ta bort. platforma launchen har ett litet utrymme på webbplatsen och gör att du snabbt kan läsa in dina sidor.

>[!IMPORTANT]
>
>Du kan inte aktivera segment för att skicka Platforma launcher, men du kan konfigurera regler så att endast händelsedata vidarebefordras i vissa situationer. Läs mer nedan.

Du kan skapa *regler* som bestämmer när händelsedata ska vidarebefordras till tillägg. Denna kraftfulla funktion gör att du bara kan vidarebefordra händelsedata i vissa situationer, i motsats till att skicka händelsedata för varje interaktion. Mer information finns i [Adobe Experience Platform Launch-dokumentationen](../../../tags/ui/managing-resources/rules.md).

## Exempel på användningsexempel för tillägg till Platforma launcher {#extensions-use-cases}

platform launch Extensions gör att ni kan tillgodose olika kundbehov. Exempel på användningsområden för Platform launch-tillägg är:

- Du kan skicka data för webbplatser eller inbyggda appar till Facebook via Facebook pixeltillägg. Facebook Pixel anger vilka delar av webbplatsen eller appen en besökare navigerade till, vidarebefordrar den informationen till Facebook och du kan rikta om besökaren via Facebook.
- Ni kan vidarebefordra händelsedata från era webbplatser och appar till Google Analytics för att analysera och fatta beslut baserat på dessa data.
- Du kan aktivera en chatbox-app på klientsidan vid rätt tidpunkt baserat på hur dina användare interagerar med dina sidor, enligt de regler du har ställt in i Platforma launchen.

## Tilläggskategorier {#extension-categories}

platforma launcher kan ingå i följande kategorier i Platform:

- [Reklam](../advertising/overview.md)
- [Analytics ](../analytics/overview.md)
- [Datahanteringsplattform](../data-management/overview.md)
- [E-postmarknadsföringsmål](../email-marketing/overview.md)
- [Personalisering](../personalization/overview.md)
- [Undersökningar](../survey/overview.md)
- [Kundens röst](../voice/overview.md)
