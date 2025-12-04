---
title: Inställningar för push-meddelanden
description: Konfigurera inställningar för push-meddelanden för Web SDK-taggtillägget.
source-git-commit: 0b3f4ec51cac182b637c79b9fcb883e5f8f78d02
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# Inställningar för push-meddelanden

>[!AVAILABILITY]
>
>Push-meddelanden för Web SDK finns för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

I det här konfigurationsavsnittet kan du ange en offentlig VAPID-nyckel för autentisering av push-meddelanden.

>[!NOTE]
>
>Den här funktionen måste först aktiveras med [anpassade byggkomponenter](custom-build-components.md). Den är inaktiverad som standard.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Expandera **[!UICONTROL Custom build components]** och aktivera sedan **[!UICONTROL Push notifications]**.
1. Under [!UICONTROL SDK instances] bläddrar du nedåt för att hitta avsnittet [!UICONTROL Push Notifications].
1. Ange den offentliga VAPID-nyckeln i fältet **[!UICONTROL VAPID Public Key]**.

![Bild som visar inställningar för push-meddelanden med hjälp av taggtillägget Web SDK](../assets/push-notifications.png)

Följande fält är tillgängliga:

## [!UICONTROL VAPID public key]

Den VAPID-offentliga nyckel som används för push-prenumerationer. Det är en Base64-kodad sträng.

## [!UICONTROL Application ID]

Program-ID som är associerat med den offentliga VAPID-nyckeln.

## [!UICONTROL Tracking dataset ID]

Datauppsättnings-ID för spårning och analys av push-meddelanden.

## Skicka meddelanden med JavaScript-biblioteket

Det här avsnittet är taggmotsvarigheten till [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) när JavaScript-biblioteket konfigureras. Den länkade sidan innehåller även information om krav och generering av en offentlig VAPID-nyckel.
