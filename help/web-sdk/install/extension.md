---
title: Installera Web SDK med hjälp av taggtillägget
description: Referera till Web SDK-biblioteket med Adobe Experience Cloud Data Collection.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Installera Web SDK med hjälp av taggtillägget

Adobe har ett dedikerat taggtillägg för att implementera och konfigurera Web SDK. Den här implementeringsmetoden är den primära metod som rekommenderas av Adobe för att distribuera och underhålla datainsamlingskod.

När du uppfyller [kraven](overview.md) kan du distribuera Web SDK-taggtillägget genom att göra följande:

## Installera tillägget i en tagg

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap eller skapa en taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och markera sedan fliken **[!UICONTROL Catalog]**.
1. Leta reda på och installera tillägget **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Välj lämplig sandlåda och datastam för varje miljö och klicka sedan på **[!UICONTROL Save]**.

Mer information finns i dokumentationen om hur du [konfigurerar Web SDK-taggtillägget](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

## Publish the tag code to development

Tillägget Web SDK är nu installerat för den här taggen. Nu kan du publicera taggkoden och använda den i en utvecklingsmiljö.

1. Navigera till **[!UICONTROL Publishing flow]** och välj sedan **[!UICONTROL Add Library]**.
1. Ge det här biblioteket valfritt namn, till exempel &quot;Lägg till Web SDK-bibliotek&quot;. Ställ in listrutan [!UICONTROL Environment] på &quot;Utveckling&quot;.
1. Välj **[!UICONTROL Add All Changed Resources]** och klicka sedan på **[!UICONTROL Save & Build to Development]**.

## Installera inläsarkoden på din plats

Nu när taggkoden har publicerats kan du lägga till tagginläsarkoden på webbplatsen.

1. Navigera till **[!UICONTROL Environments]** och klicka sedan på Box-ikonen bredvid&quot;Development&quot; för att öppna ett modalt fönster som innehåller installationsanvisningar för den här miljön.
1. Kopiera inbäddningskoden och klistra in den i taggen `<head>` på webbplatsen.

## Fyll i implementeringen och publicera i produktionen

Mer information om själva tillägget finns i översikten för [Web SDK-tillägget](../../tags/extensions/client/web-sdk/overview.md) och i översikten för [taggar](../../tags/home.md) finns mer information om hur du navigerar i tagggränssnittet.
