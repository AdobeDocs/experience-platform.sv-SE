---
title: Installera Web SDK med hjälp av taggtillägget
description: Referera till Web SDK-biblioteket med Adobe Experience Cloud Data Collection.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Installera Web SDK med hjälp av taggtillägget

Adobe har ett dedikerat taggtillägg för att implementera och konfigurera Web SDK. Den här implementeringsmetoden är den primära metod som rekommenderas av Adobe för att distribuera och underhålla datainsamlingskod.

När du mött [krav](overview.md)kan du distribuera taggtillägget för Web SDK genom att göra så här:

## Installera tillägget i en tagg

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap eller skapa en taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** väljer du **[!UICONTROL Catalog]** -fliken.
1. Leta rätt på och installera **[!UICONTROL Adobe Experience Platform Web SDK]** tillägg.
1. Välj lämplig sandlåda och datastam för varje miljö och klicka sedan på **[!UICONTROL Save]**.

## Publicera koden för utveckling

Tillägget Web SDK är nu installerat för den här taggen. Nu kan du publicera taggkoden och använda den i en utvecklingsmiljö.

1. Navigera till **[!UICONTROL Publishing flow]** väljer **[!UICONTROL Add Library]**.
1. Ge det här biblioteket valfritt namn, till exempel &quot;Lägg till Web SDK-bibliotek&quot;. Ange [!UICONTROL Environment] nedrullningsbar meny till &quot;Utveckling&quot;.
1. Välj **[!UICONTROL Add All Changed Resources]** och sedan klicka **[!UICONTROL Save & Build to Development]**.

## Installera inläsarkoden på din plats

Nu när taggkoden har publicerats kan du lägga till tagginläsarkoden på webbplatsen.

1. Navigera till **[!UICONTROL Environments]** klickar du sedan på Box-ikonen bredvid&quot;Utveckling&quot; för att öppna ett modalt fönster med installationsanvisningar för den här miljön.
1. Kopiera inbäddningskoden och klistra in den i `<head>` -tagg för din webbplats.

## Fyll i implementeringen och publicera i produktionen

Se [Översikt över Web SDK-tillägg](../../tags/extensions/client/web-sdk/overview.md) för mer information om själva tillägget, och [Översikt över taggar](../../tags/home.md) om du vill ha mer information om hur du navigerar i tagggränssnittet.
