---
title: Konfigurationsinställningar för direktuppspelande media
description: Anpassa hur webbfilens SDK-taggtillägg samlar in strömmande mediedata.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Konfigurationsinställningar för direktuppspelande media

Funktionen för mediainsamling hjälper dig att samla in data relaterade till mediesessioner, till exempel medieuppspelningar, pauser, slutföranden och andra relaterade händelser. När de samlats in kan du skicka dessa data till Adobe Experience Platform eller Adobe Analytics för att generera rapporter. Den här funktionen är en heltäckande lösning för att spåra och förstå hur medieanvändningen fungerar på din webbplats.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Streaming media]**.

![Bild som visar inställningarna för mediesamlingen för SDK-taggtillägget Web i tagggränssnittet](../assets/media-collection.png)

## Förhandskrav

För att kunna använda komponenten för direktuppspelande media i Web SDK måste du uppfylla följande krav:

* Se till att du har tillgång till Adobe Experience Platform eller Adobe Analytics.
* Aktivera alternativet **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** för den datastream som du använder.
* Kontrollera att schemat som används av din datastream innehåller schemafälten för mediesamlingen.
* Konfigurera funktionen för direktuppspelning av media i taggtillägget Web SDK, som visas på den här sidan.

## [!UICONTROL Channel]

Namnet på den kanal där mediesamlingen sker. Exempel: `Video channel`. Alla strängvärden är giltiga.

## [!UICONTROL Player Name]

Namnet på den mediespelare som egenskapen använder för medieuppspelning.

## [!UICONTROL Application Version]

Den version av mediespelarprogrammet som egenskapen använder för medieuppspelning.

## [!UICONTROL Main ping interval]

Fästfrekvensen för huvudinnehållet, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `10` och `50` sekunder. Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](/help/collection/js/commands/createmediasession.md#automatic) används.

## [!UICONTROL Ad ping interval]

Frekvensen för pingar för annonsinnehåll, i sekunder. Standardvärdet är `10`. Värdena kan ligga mellan `1` och `10` sekunder. Om inget värde anges används standardvärdet när [automatiskt spårade sessioner](/help/collection/js/commands/createmediasession.md#automatic) används.
