---
title: Avancerade konfigurationsinställningar
description: Konfigurera avancerade inställningar för taggtillägget Web SDK.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---

# Avancerade konfigurationsinställningar

I det här konfigurationsavsnittet kan du ändra avancerade inställningar. Adobe rekommenderar att du låter dessa alternativ vara som de är för de flesta implementeringar.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet **[!UICONTROL Advanced Settings]**.

![Bild som visar de avancerade inställningarna på SDK-tilläggssidan för webbtaggar](../assets/advanced-settings.png)

Det finns för närvarande ett alternativ.

## [!UICONTROL Edge base path]

Använd det här fältet om du vill ändra den grundsökväg som används för att interagera med Edge Network. Adobe kan begära att du ändrar det här fältet om du deltar i vissa alfa- eller betatester. I annat fall rekommenderar Adobe att du låter det behålla standardvärdet `ee`.

Det här fältet är taggmotsvarigheten till [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) när JavaScript-biblioteket konfigureras.
