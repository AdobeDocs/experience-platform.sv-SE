---
title: pushNotifications
description: Konfigurera push-meddelanden för Web SDK för att aktivera webbläsarbaserade push-meddelanden.
source-git-commit: 7c2afd6d823ebb2db0fabb4cc16ef30bcbfeef13
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 1%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Push-meddelanden för Web SDK finns för närvarande i **beta**. Funktionen och dokumentationen kan ändras.

Med egenskapen `pushNotifications` kan du konfigurera push-meddelanden för webbprogram. Med den här funktionen kan webbprogrammet ta emot meddelanden som har skickats från en server, även när webbplatsen inte har lästs in i webbläsaren.

## Förhandskrav {#prerequisites}

Innan du konfigurerar push-meddelanden måste du se till att:

1. **Användarbehörighet**: Användare måste uttryckligen ge behörighet för meddelanden
2. **Tjänstarbetare**: En registrerad tjänstarbetare krävs för att push-meddelanden ska fungera
3. **VAPID-nycklar**: Generera VAPID-nycklar (Voluntary Application Server Identification) för säker kommunikation
4. **Program-ID**: Program-ID:t som används när VAPID-nycklarna sparas i Adobe Journey Optimizer -> Kanaler -> Push-inställningar -> Push-autentiseringsuppgifter
5. **Datauppsättnings-ID för spårning**: ID:t för systemdatauppsättningen med namnet&quot;AJO Push Tracking Experience Event Dataset&quot;. Hämta detta från Adobe Journey Optimizer -> Dataset

## Generera VAPID-nycklar {#generate-vapid-keys}

Om du vill generera VAPID-nycklar installerar du NPM-paketet `web-push` och kör:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Detta genererar ett nyckelpar för offentlig och privat nyckel. Använd den offentliga nyckeln i din Web SDK-konfiguration och lagra den privata nyckeln i Adobe Journey Optimizer push-meddelandekanal.

## Installera servicearbetaren JavaScript

Tjänstarbetarens kod måste hanteras från samma domän som webbplatsen. Hämta koden för servicearbetare från Adobe CDN och lagra sedan JavaScript-filen på din egen server. Koden för Web SDK-tjänstarbetare är tillgänglig med följande URL-struktur:

- **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Fullständig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Här följer ett exempel på hur du installerar servicearbetaren:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Konfigurera push-meddelanden med hjälp av taggtillägget Web SDK {#configure-push-notifications-tag-extension}

Följ de här stegen för att aktivera och konfigurera push-meddelanden:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Aktivera **[!UICONTROL Custom build components]** i avsnittet **[!UICONTROL Push notifications]**.
1. Bläddra nedåt för att hitta avsnittet [!UICONTROL Push Notifications].
1. Ange den offentliga VAPID-nyckeln i fältet **[!UICONTROL VAPID Public Key]**.
1. Ange ditt program-ID i fältet **[!UICONTROL Application ID]**.
1. Ange ditt ID för spårningsdatauppsättning i fältet **[!UICONTROL Tracking Dataset ID]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

>[!NOTE]
>
> Push-meddelanden måste aktiveras explicit i taggens tilläggskonfiguration. Funktionen är inaktiverad som standard.

## Konfigurera push-meddelanden med Web SDK JavaScript-biblioteket {#configure-push-notifications-javascript}

Ange objektet `pushNotifications` när du kör kommandot `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Egenskaper {#properties}

| Egenskap | Typ | Obligatoriskt | Beskrivning |
|---------|----|---------|-----------|
| `vapidPublicKey` | Sträng | Ja | Den VAPID-offentliga nyckel som används för push-prenumeration. Måste vara en Base64-kodad sträng. |
| `applicationId` | Sträng | Ja | Program-ID som är associerat med den här offentliga VAPID-nyckeln. |
| `trackingDatasetId` | Sträng | Ja | Det systemdatauppsättnings-ID som används för spårning av push-meddelanden. |

## Viktiga överväganden {#important-considerations}

- **Säkerhet**: Push-prenumerationer är kopplade till den specifika VAPID-offentliga nyckeln som används under prenumerationen. Om du ändrar VAPID-nycklar kommer befintliga prenumerationer automatiskt att avbrytas och återskapas med den nya nyckeln.
- **Cachelagring**: SDK hanterar automatiskt prenumerationsuppdateringar genom att jämföra den aktuella ECID- och prenumerationsinformationen med cachelagrade värden. Prenumerationsdata skickas endast när ändringar identifieras.
- **Krav för servicearbetare**: Push-meddelanden kräver en registrerad servicearbetare. Kontrollera att din servicearbetare är korrekt konfigurerad för att hantera push-händelser.

## Nästa steg {#next-steps}

När du har konfigurerat push-meddelanden använder du kommandot [`sendPushSubscription`](../sendPushSubscription.md) för att registrera push-prenumerationer hos Adobe Experience Platform.
