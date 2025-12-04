---
title: sendPushSubscription
description: Registrera prenumerationer på push-meddelanden hos Adobe Experience Platform.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>Push-meddelanden för Web SDK finns för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

Kommandot `sendPushSubscription` registrerar push-meddelandeprenumerationer hos Adobe Experience Platform. Det här kommandot hanterar hämtning av information om push-prenumerationer från webbläsaren och skickar dem till din konfigurerade datastam. Den finns i Web SDK version 2.29.0 eller senare.

## Förhandskrav {#prerequisites}

Kontrollera att du har:`sendPushSubscription`

1. **Konfigurerade push-meddelanden**: Konfigurera konfigurationsegenskapen [`pushNotifications`](configure/pushnotifications.md) med den offentliga VAPID-nyckeln
2. **Användarbehörighet**: Användarna måste ha beviljat aviseringsbehörighet (`Notification.permission === "granted"`)
3. **Tjänstarbetare**: En registrerad servicearbetare måste vara tillgänglig på din plats
4. **Stöd för Push Manager**: Webbläsaren måste ha stöd för push-meddelanden och PushManager API är tillgängligt

Kör kommandot `sendPushSubscription` när du anropar den konfigurerade instansen av Web SDK. Kontrollera att du anropar kommandot [`configure`](configure/overview.md) med push-meddelanden konfigurerade innan du anropar kommandot `sendPushSubscription`.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Rekommenderad exekveringsfrekvens {#recommended-execution-frequency}

Adobe rekommenderar att du kör `sendPushSubscription`-kommandot **en gång om dagen** för att få optimal push-meddelandefunktion. Denna frekvens säkerställer att

* Prenumerationsinformationen är fortfarande aktuell i Adobe Experience Platform
* Alla ändringar av push-token eller prenumerationsstatus registreras
* Användarprofilen uppdateras med de senaste inställningarna för push-meddelanden

Du kan implementera detta med en metod som liknar den nedan:

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Så fungerar det {#how-it-works}

Kommandot `sendPushSubscription` utför följande åtgärder:

1. **Verifierar krav**: Verifierar att push-meddelanden har konfigurerats och användarbehörighet har beviljats
2. **Meddelar identitet**: Väntar på att användarens ECID ska vara tillgängligt
3. **Hämtar prenumeration**: Hämtar den aktiva push-prenumerationen från servicearbetaren med den konfigurerade VAPID-nyckeln
4. **Söker efter ändringar**: Jämför aktuell prenumerationsinformation med cachelagrade värden (ECID + prenumerationsinformation). Om prenumerationsinformationen inte har ändrats loggar kommandot ett informationsmeddelande och returnerar det utan att göra någon nätverksbegäran
5. **Skickar till datastream**: Om ändringar identifieras, överför prenumerationsdata till din konfigurerade Adobe Experience Platform-datastream
6. **Uppdateringscache**: Lagrar den nya prenumerationsinformationen för framtida jämförelse

## Felhantering {#error-handling}

Vanliga feltillstånd och deras meddelanden:

| Fel | Orsak |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | PushNotifications-konfiguration saknas eller är ogiltig |
| `"Service workers are not supported in this browser."` | Webbläsaren stöder inte servicearbetare |
| `"Push notifications are not supported in this browser."` | Webbläsaren stöder inte push-meddelanden eller meddelande-API |
| `"The user has not given permission to send push notifications."` | Användaren har inte beviljat aviseringsbehörighet (`Notification.permission === "granted"`) |
| `"No service worker registration was found."` | Ingen servicearbetare har registrerats för aktuellt ursprung |
| `"No VAPID public key was provided."` | Den offentliga VAPID-nyckeln saknas i konfigurationen |

## Datanyttolast {#data-payload}

Kommandot skickar push-meddelandedata i följande format:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Registrera push-prenumerationer med hjälp av taggtillägget Web SDK {#register-push-subscription-tag-extension}

Webbtaggtillägget för SDK som är ekvivalent med det här fältet använder åtgärden [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) i en taggregel.

>[!MORELIKETHIS]
>
>* [Konfigurera push-meddelanden](configure/pushnotifications.md)
>* [API-specifikation för Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
