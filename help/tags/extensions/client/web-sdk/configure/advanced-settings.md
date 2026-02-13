---
title: Avancerade konfigurationsinställningar
description: Konfigurera avancerade inställningar för taggtillägget Web SDK.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Avancerade konfigurationsinställningar {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Avancerade inställningar"
>abstract="Avancerade konfigurationsinställningar. Adobe rekommenderar att du låter dessa alternativ vara som de är för de flesta implementeringar."

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
