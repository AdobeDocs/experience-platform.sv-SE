---
keywords: taggtillägg;taggtillägg;startmål; plattformstaggtillägg;plattformstaggtillägg;platforma launchens mål
title: Taggtillägg i Adobe Experience Platform
description: Adobe Experience Platform erbjuder nästa generation tagghanteringsfunktioner från Adobe. Med Platform får ni ett enkelt sätt att driftsätta och hantera alla de analyser, marknadsförings- och annonstaggar som behövs för att skapa relevanta kundupplevelser.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Tagga tillägg i Adobe Experience Platform

Adobe Experience Platform erbjuder nästa generation tagghanteringsfunktioner från Adobe. Med Platform får ni ett enkelt sätt att driftsätta och hantera alla de analyser, marknadsförings- och annonstaggar som behövs för att skapa relevanta kundupplevelser. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde.

En introduktion till taggar finns i resurserna nedan:

- [Översikt över taggar](../../../tags/home.md)
- [Snabbstartsguide](../../../tags/quick-start/quick-start.md)

## Hitta taggtillägg i plattformsgränssnittet {#how-to-find-extensions-in-interface}

Om du vill hitta tilläggen i plattformsgränssnittet går du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** och väljer **[!UICONTROL Extensions]** i filtret **[!UICONTROL Types]**.

![Filtret Tillägg i gränssnittet](../../assets/catalog/launch-extensions/filter.png)

## Så här fungerar taggtillägg {#how-extensions-work}

Tillägg vidarebefordrar råa händelsedata till flera typer av destinationer. Tänk på tillägg som en **typ av händelsespårning**-typ av mål. Detta är en enklare typ av integrering med målplattformar, som bara vidarebefordrar råhändelsedata. Exempel på sådana är [tillägget för Gainsight-anpassning](../personalization/gainsight.md) eller [Bekräfta röst för kundtillägget](../voice/confirmit-digital-feedback.md).

**Profil-/** segmentexportdestinationer i Adobe Experience Platform samlar in händelsedata, kombinerar dem med andra datakällor, tillämpar segmentering och exporterar segment och kvalificerade profiler till destinationer. Exempel på sådana är [Amazon S3-molnlagringsmålet](../cloud-storage/amazon-s3.md) eller [Google Display &amp; Video 360-annonsmålet](../advertising/google-dv360.md).

![Märkordstillägg jämfört med andra mål](../../assets/common/launch-and-other-destinations.png)

## Fördelar med att använda taggtillägg {#extensions-benefits}

Plattformens taggfunktioner är kostnadsfria för befintliga Experience Cloud-kunder. Systemet förenklar taggdistribution på din webbplats med lättanvända tillägg som du kan installera, konfigurera, uppdatera och ta bort. Taggar gör att det inte finns så mycket plats på webbplatsen och gör att du snabbt kan läsa in sidorna.

Du kan inte aktivera segment för taggtillägg, men du kan konfigurera regler så att endast händelsedata vidarebefordras i vissa situationer. Denna kraftfulla funktion gör att du bara kan vidarebefordra händelsedata i vissa situationer, i motsats till att skicka händelsedata för varje interaktion. Mer information finns i [taggdokumentationen](../../../tags/ui/managing-resources/rules.md) om regler.

## Exempel på användningsexempel för tillägg {#extensions-use-cases}

Med tillägg kan ni tillgodose olika kundbehov. Exempel på användningsområden för tillägg är:

- Du kan skicka data för webbplatser eller inbyggda appar till Facebook via Facebook pixeltillägg. Facebook Pixel anger vilka delar av webbplatsen eller appen en besökare navigerade till, vidarebefordrar den informationen till Facebook och du kan rikta om besökaren via Facebook.
- Ni kan vidarebefordra händelsedata från era webbplatser och appar till Google Analytics för att analysera och fatta beslut baserat på dessa data.
- Du kan aktivera en chatbox-app på klientsidan vid rätt tidpunkt baserat på hur dina användare interagerar med dina sidor, enligt de regler du har ställt in.

## Tilläggskategorier {#extension-categories}

Tillägg kan delas in i följande kategorier i Plattform:

- [Reklam](../advertising/overview.md)
- [Analytics ](../analytics/overview.md)
- [Datahanteringsplattform](../data-management/overview.md)
- [E-postmarknadsföringsmål](../email-marketing/overview.md)
- [Personalisering](../personalization/overview.md)
- [Undersökningar](../survey/overview.md)
- [Kundens röst](../voice/overview.md)
