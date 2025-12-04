---
title: Hämta spåraren för Media Analytics
description: Exporterar det äldre medie-API:t till ett fönsterobjekt.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Hämta Media Analytics Tracker

Åtgärden **[!UICONTROL Get Media Analytics tracker]** används för att hämta API:t för äldre medieanalys. När åtgärden konfigureras och ett objektnamn anges, exporteras det gamla Media Analytics-API:t till det fönsterobjektet. Den här åtgärden är användbar för att gå från äldre Media Analytics till Streaming Media Analytics.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ sedan in [!UICONTROL Action type] på **[!UICONTROL Get Media Analytics tracker]**.

![Experience Platform-gränssnittsbild som visar åtgärdstypen Get Media Analytics Tracker.](../assets/get-media-analytics-tracker.png)

Den här åtgärden innehåller ett enda fält som du kan konfigurera:

* **[!UICONTROL Export the Media Legacy API to this window object]**: Markerar det objekt som du vill exportera Media Legacy API till. Om ingen anges exporteras API:t till `window.Media`.
