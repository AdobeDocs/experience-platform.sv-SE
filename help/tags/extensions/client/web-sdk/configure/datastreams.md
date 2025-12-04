---
title: Konfigurationsinställningar för dataström
description: Konfigurera dataströmmen för att skicka data till med hjälp av webbfilens SDK-taggtillägg.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Konfigurationsinställningar för dataström

I det här konfigurationsavsnittet kan du avgöra vilken [datastream](/help/datastreams/overview.md) som du vill skicka data till. **Ett datastream-ID krävs för alla data som skickas till Edge Network.**

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Datastreams]**.

![Bild som visar datastream-inställningarna för Web SDK-taggtillägget i tagggränssnittet](../assets/web-sdk-ext-datastreams.png)

När du väljer datastreams kan du göra det för varje [miljö](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging] och [!UICONTROL Production]). Dessa fält är värdefulla när du vill separera data som skickas mellan utvecklings-, staging- och produktionsmiljöer. Det ger ett smidigt arbetsflöde där du inte behöver bekymra dig om att skicka data till fel datastream, så länge du installerar rätt tagginläsare i varje miljö.

Du kan fylla i dataStream-ID:n på något av följande sätt:

* **[!UICONTROL Choose from list]**: Varje miljö innehåller två nedrullningsbara menyer, som gör att du kan välja sandlådan och datastream för den valda miljön. Värdena i varje nedrullningsbar meny beror på dina konfigurerade [datastreams](/help/datastreams/overview.md) i respektive [sandlåda](/help/sandboxes/ui/overview.md).

* **[!UICONTROL Enter values]**: I stället för att använda nedrullningsbara menyer för att välja önskat dataström kan du ange önskat dataström-ID manuellt direkt. I varje miljö kan du ange ett dataström-ID direkt eller fylla i det här fältet med ett [dataelement](/help/tags/ui/managing-resources/data-elements.md).
