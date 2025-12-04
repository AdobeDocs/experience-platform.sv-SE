---
title: Konfigurationsinställningar för SDK-instanser
description: Konfigurera allmänna inställningar för Web SDK-instansen.
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# Konfigurationsinställningar för SDK-instanser

Det här konfigurationsavsnittet styr Web SDK-instansnamnet, IMS-organisationen som det gäller för och platsen som du vill skicka data till. Som standard har en instans namnet `alloy`.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och välj sedan **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Leta reda på instansnamnet precis nedanför det utökade [!UICONTROL SDK instances]-dragspelet.

![Bild som visar de allmänna inställningarna för SDK-taggtillägget för webben i användargränssnittet för taggar](../assets/web-sdk-ext-general.png)

Följande alternativ är tillgängliga:

## [!UICONTROL Name]

Taggtillägget Adobe Experience Platform Web SDK har stöd för flera instanser på sidan. Namnet används för att skicka data till flera organisationer utan att dubbla SDK-taggbibliotek krävs. Du kan ändra instansnamnet till ett giltigt JavaScript-objektnamn.

## [!UICONTROL IMS organization ID]

ID:t för organisationen som du vill att data ska skickas till på Adobe. För det mesta använder du standardvärdet som fylls i automatiskt. När du har flera instanser på sidan fyller du i det här fältet med värdet för den andra organisationen som du vill skicka data till.

## [!UICONTROL Edge domain]

Domänen som tillägget skickar och tar emot data från. Standardvärdet för `edge.adobedc.net` fungerar, men i de flesta fall bör du använda en förstahandsdomän. Se det [Adobe-hanterade certifikatprogrammet](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) för instruktioner om hur du konfigurerar en förstahandsdomän som passar för datainsamling. Se även [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) i dokumentationen för JavaScript-biblioteket för vägledning om hur du anger det här värdet.
