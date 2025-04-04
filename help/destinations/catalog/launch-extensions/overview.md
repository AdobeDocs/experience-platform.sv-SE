---
keywords: taggtillägg;taggtillägg;startmål;plattformstaggtillägg;plattformstaggtillägg;plattformens startmål
title: Taggtillägg i Adobe Experience Platform
description: Adobe Experience Platform erbjuder nästa generations tagghanteringsfunktioner från Adobe. Experience Platform ger er ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att skapa relevanta kundupplevelser.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Tagga tillägg i Adobe Experience Platform

Adobe Experience Platform erbjuder nästa generations tagghanteringsfunktioner från Adobe. Experience Platform ger er ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att skapa relevanta kundupplevelser. Adobe Experience Cloud-kunder får taggar som en inkluderad funktion som ger mervärde.

En introduktion till taggar finns i resurserna nedan:

- [Översikt över taggar](../../../tags/home.md)
- [Snabbstartsguide](../../../tags/quick-start/quick-start.md)

## Hitta taggtillägg i Experience Platform-gränssnittet {#how-to-find-extensions-in-interface}

Om du vill hitta tilläggen i Experience Platform-gränssnittet bläddrar du till **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** och väljer **[!UICONTROL Extensions]** i filtret **[!UICONTROL Types]**.

![Filtret Tillägg i gränssnittet](../../assets/catalog/launch-extensions/filter.png)

## Så här fungerar taggtillägg {#how-extensions-work}

Ett [taggtillägg](../../../tags/home.md#extensions) är ett kodpaket som förbättrar funktionerna för en webbplats eller mobilapp. Detta kan inkludera att skicka råhändelsedata till ett mål som [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md), men de kan även hantera andra funktioner.

Det är viktigt att skilja mellan tillägg för tagg- och händelsevidarebefordran. De tillägg som visas i Experience Platform målanvändargränssnitt är *taggtillägg*. Mer information om [skillnaderna mellan taggar och händelsevidarebefordran](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags) finns i översikten över händelsevidarebefordran.



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Fördelar med att använda taggtillägg {#extensions-benefits}

Experience Platform taggfunktioner är kostnadsfria för befintliga Experience Cloud-kunder. Systemet förenklar taggdistribution på din webbplats med lättanvända tillägg som du kan installera, konfigurera, uppdatera och ta bort. Taggar gör att det inte finns så mycket plats på webbplatsen och gör att du snabbt kan läsa in sidorna.

Du kan inte aktivera målgrupper för taggtillägg, men du kan konfigurera regler så att endast händelsedata vidarebefordras i vissa situationer. Denna kraftfulla funktion gör att du bara kan vidarebefordra händelsedata i vissa situationer, i motsats till att skicka händelsedata för varje interaktion. Mer information finns i reglerna i [taggdokumentationen](../../../tags/ui/managing-resources/rules.md).

## Exempel på användningsexempel för tillägg {#extensions-use-cases}

Med tillägg kan ni tillgodose olika kundbehov. Exempel på användningsområden för tillägg är:

- Du kan skicka webbplatsdata eller inbyggda appdata till Facebook via Facebook-pixeltillägget. Facebook Pixel anger vilka delar av din webbplats eller app en besökare navigerade till, vidarebefordrar den informationen till Facebook och du kan återannonsera besökaren via Facebook.
- Ni kan vidarebefordra händelsedata från era webbplatser och appar till Google Analytics för att analysera och fatta beslut baserat på dessa data.
- Du kan aktivera en chatbox-app på klientsidan vid rätt tidpunkt baserat på hur dina användare interagerar med dina sidor, enligt de regler du har ställt in.

## Tilläggskategorier {#extension-categories}

Tillägg kan delas in i följande kategorier i Experience Platform:

- [Advertising](../advertising/overview.md)
- [Analytics ](../analytics/overview.md)
- [Datahanteringsplattform](../data-management/overview.md)
- [E-postmarknadsföringsmål](../email-marketing/overview.md)
- [Personalisering](../personalization/overview.md)
- [Undersökningar](../survey/overview.md)
- [Kundens röst](../voice/overview.md)
