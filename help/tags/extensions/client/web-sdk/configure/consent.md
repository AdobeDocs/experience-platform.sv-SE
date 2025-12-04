---
title: Inställningar för konfiguration av samtycke
description: Konfigurera standardinställningar för samtycke och sekretess för taggtillägget.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# Inställningar för konfiguration av samtycke

I avsnittet **[!UICONTROL Consent]** kan du välja standardnivån för samtycke som antas om ingen annan explicit medgivandeinställning anges. Standardmedgivandenivå sparas inte i användarprofiler.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Consent]**.

![Bild som visar sekretessinställningarna för SDK-taggtillägget Web i användargränssnittet för taggar](../assets/web-sdk-ext-privacy.png)

Det här avsnittet innehåller en enda uppsättning alternativknappar som fastställer standardmedgivandenivån:

* **[!UICONTROL In]**: Samla in händelser som inträffar innan användaren ger sitt medgivande.
* **[!UICONTROL Out]**: Släpp händelser som inträffar innan användaren ger sitt medgivande.
* **[!UICONTROL Pending]**: Köhändelser som inträffar innan användaren ger sitt samtycke. När medgivande ges skickas händelser i kö till Adobe. När samtycke nekas ignoreras händelser i kö.
* **[!UICONTROL Provide a data element]**: Välj ett dataelement som bestämmer någon av ovanstående konfigurationsinställningar. Giltiga värden är strängarna `"in"`, `"out"` eller `"pending"`.

Om din organisation kräver uttryckligt tillstånd från användaren för att samla in data, rekommenderar Adobe att du anger standardsamtycke till antingen **[!UICONTROL Out]** eller **[!UICONTROL Pending]**.
