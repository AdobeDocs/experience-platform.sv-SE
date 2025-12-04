---
title: Skicka push-prenumeration
description: Registrera, skicka och samla in data för push-prenumerationer i webbläsare.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Skicka push-prenumeration

>[!AVAILABILITY]
>
>Push-meddelanden för Web SDK finns för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

Åtgärden **[!UICONTROL Send push subscription]** registrerar push-meddelandeprenumerationer hos Adobe Experience Platform. Den hanterar hämtning av information om push-prenumerationer från webbläsaren och skickar dem till din konfigurerade datastam. Den finns i Web SDK-tilläggsversion 2.32.0 eller senare.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send push subscription]**.

Åtgärden har inga konfigurationsinställningar förutom att markera en SDK-instans.

Se till att du anger en giltig offentlig [VAPID](../configure/push-notifications.md) när du konfigurerar tillägget innan du använder det här kommandot.

Den här åtgärden är taggtillägget som motsvarar kommandot [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). På den länkade sidan finns information om krav, rekommenderad körningsfrekvens, hur kommandot fungerar och felhantering.

>[!MORELIKETHIS]
>
>* [Konfigurera push-meddelanden](../configure/push-notifications.md)
>* [API-specifikation för Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
