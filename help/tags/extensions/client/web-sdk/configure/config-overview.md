---
title: Översikt över konfigurationsinställningar
description: Läs om tillgängliga alternativ när du konfigurerar taggtillägget för Web SDK.
exl-id: 03f7bc0a-05c9-48ae-ae57-478db6d18f52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---

# Översikt över konfigurationsinställningar {#config-overview}

Taggtillägget Adobe Experience Platform Web SDK innehåller flera alternativ som du kan anpassa. De här konfigurationsinställningarna motsvarar taggen [`configure`](/help/collection/js/commands/configure/overview.md) i JavaScript-biblioteket.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.

## Anpassade byggkomponenter

Om optimering av byggstorlek är en prioritet för din organisation kan du inaktivera vissa funktioner som du inte använder för att minska tilläggets byggstorlek. Mer information finns i [Anpassade byggkomponenter](custom-build-components.md).

## SDK-instanser

De flesta implementeringar behöver vanligtvis en enda SDK-instans. Om din organisation kräver flera Web SDK-spårningsinstanser kan du använda knappen **[!UICONTROL Add instance]**. Följande övergripande avsnitt är tillgängliga när du konfigurerar varje instans av Web SDK-taggar:

* [**[!UICONTROL SDK instance]**](general.md): Allmänna inställningar för instansen. Alla fält i det här avsnittet är obligatoriska.
* [**[!UICONTROL Datastreams]**](datastreams.md): Där du vill att data ska placeras för varje taggmiljö.
* [**[!UICONTROL Consent]**](consent.md): Standardinställningar för godkännande för tillägget.
* [**[!UICONTROL Identity]**](identity.md): Migreringsinställningar för cookie och besökare.
* [**[!UICONTROL Personalization]**](personalization.md): Anpassa besökarupplevelsen på individnivå.
* [**[!UICONTROL Data collection]**](data-collection.md): Inkludera eller utelämna det som samlas in automatiskt.
* [**[!UICONTROL Streaming media]**](streaming-media.md): Inställningar som är specifika för direktuppspelad mediesamling.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): Ändra konfigurationsinställningar när vissa villkor uppfylls.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): Ange grundsökvägen för Edge Network.
