---
title: Inställningar för push-meddelanden
description: Konfigurera inställningar för push-meddelanden för Web SDK-taggtillägget.
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# Inställningar för push-meddelanden {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="Push-meddelanden"
>abstract="Anger en offentlig VAPID-nyckel för autentisering av push-meddelanden."

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
