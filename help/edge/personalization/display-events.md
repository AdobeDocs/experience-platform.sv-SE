---
title: Hantera visningshändelser i Web SDK
description: I den här artikeln förklaras vad som är visningshändelser och hur du kan använda dem i Web SDK.
source-git-commit: da506cd5de69047e326790d0fae56f76c728e7a5
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Hantera visningshändelser i Web SDK

Visningshändelser används av Web SDK för att informera din personaliserings- eller analystjänst när ett visst personaliseringsinnehåll visas på en sida.

Genom att skicka visningshändelser förbättras noggrannheten i mätvärdena för personalisering och du får en korrekt översikt över vad användarna ser på sidan.

Med Web SDK kan du skicka visningshändelser på två sätt:

* [Automatiskt](#send-automatically), omedelbart efter att det personaliserade innehållet återges på sidan. Läs dokumentationen om hur du [återge personaliserat innehåll](rendering-personalization-content.md) för mer information.
* [Manuellt](#send-sendEvent-calls), via efterföljande `sendEvent` samtal.

>[!NOTE]
>
>Visningshändelser skickas inte automatiskt när användaren anropar `applyPropositions` funktion.

## Skicka visningshändelser automatiskt {#send-automatically}

När du skickar visningshändelser får du automatiskt mer korrekta analysmått, eftersom händelsen skickas omedelbart efter att personaliseringen har lästs in. Den här implementeringen har också en effektivare implementeringsmetod.

Om du vill skicka visningshändelser automatiskt när det anpassade innehållet återges på sidan måste du konfigurera följande parametrar:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` eller inte angivet

Web SDK skickar visningshändelserna omedelbart efter att en personalisering har renderats som ett resultat av en `sendEvent` ring.

## Skicka visningshändelser i efterföljande sendEvent-anrop {#send-sendEvent-calls}

Jämfört med [automatiskt](#send-automatically) skicka visningshändelser, när du inkluderar dem i efterföljande `sendEvent` kan du även ta med mer information om sidinläsningen i samtalet. Det kan vara extra information som inte var tillgänglig när det personliga innehållet begärdes.

Dessutom skickar du visningshändelser i `sendEvent` anrop minimerar avkodningsfel när Adobe Analytics används.

>[!IMPORTANT]
>
>När du använder manuellt återgivna profiler stöds visningshändelser endast via `sendEvent` samtal. I det här fallet kan du inte skicka visningshändelser automatiskt.

### Skicka visningshändelser för automatiskt återgivna förslag {#auto-rendered-propositions}

Om du vill skicka visningshändelser för automatiskt återgivna profiler måste du konfigurera följande parametrar i `sendEvent` ring:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` för sidträffens överkant

Om du vill skicka visningshändelser ringer du `sendEvent` med `personalization.includePendingDisplayNotifications: true`

### Skicka visningshändelser för manuellt återgivna förslag {#manually-rendered-propositions}

Om du vill skicka visningshändelser för manuellt återgivna utkast måste du inkludera dem i `_experience.decisioning.propositions` XDM-fält, inklusive `id`, `scope`och `scopeDetails` fält från förslagen.

Dessutom anger du `include _experience.decisioning.propositionEventType.display` fält till `1`.