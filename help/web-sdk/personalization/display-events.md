---
title: Hantera visningshändelser i Web SDK
description: I den här artikeln förklaras vad som är visningshändelser och hur du kan använda dem i Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Hantera visningshändelser i Web SDK

Visningshändelser används av Web SDK för att informera din personaliserings- eller analystjänst när ett visst personaliseringsinnehåll visas på en sida.

Genom att skicka visningshändelser förbättras noggrannheten i mätvärdena för personalisering och du får en korrekt översikt över vad användarna ser på sidan.

Med Web SDK kan du skicka visningshändelser på två sätt:

* [Automatiskt](#send-automatically), omedelbart efter att det anpassade innehållet återges på sidan. Mer information finns i dokumentationen om hur du [återger anpassat innehåll](rendering-personalization-content.md).
* [Manuellt](#send-sendEvent-calls), genom efterföljande `sendEvent` anrop.

>[!NOTE]
>
>Visningshändelser skickas inte automatiskt när funktionen `applyPropositions` anropas.

## Skicka visningshändelser automatiskt {#send-automatically}

När du skickar visningshändelser får du automatiskt mer korrekta analysmått, eftersom händelsen skickas omedelbart efter att personaliseringen har lästs in. Den här implementeringen har också en effektivare implementeringsmetod.

Om du vill skicka visningshändelser automatiskt när det anpassade innehållet återges på sidan måste du konfigurera följande parametrar:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` eller inte angivet

Web SDK skickar visningshändelserna omedelbart efter att någon personalisering har renderats som ett resultat av ett `sendEvent`-anrop.

## Skicka visningshändelser i efterföljande sendEvent-anrop {#send-sendEvent-calls}

Jämfört med att [automatiskt](#send-automatically) skickar visningshändelser kan du även inkludera mer information om sidinläsningen i anropet när du tar med dem i efterföljande `sendEvent` samtal. Det kan vara extra information som inte var tillgänglig när det personliga innehållet begärdes.

Om du skickar visningshändelser i `sendEvent` anrop minimeras dessutom avhoppsfrekvensen när du använder Adobe Analytics.

>[!IMPORTANT]
>
>När du använder manuellt återgivna profiler stöds endast visningshändelser via `sendEvent` anrop. I det här fallet kan du inte skicka visningshändelser automatiskt.

### Skicka visningshändelser för automatiskt återgivna förslag {#auto-rendered-propositions}

Om du vill skicka visningshändelser för automatiskt återgivna profiler måste du konfigurera följande parametrar i `sendEvent`-anropet:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` för sidträffens överkant

Om du vill skicka visningshändelser anropar du `sendEvent` med `personalization.includeRenderedPropositions: true`

### Skicka visningshändelser för manuellt återgivna förslag {#manually-rendered-propositions}

Om du vill skicka visningshändelser för manuellt återgivna utkast måste du inkludera dem i `_experience.decisioning.propositions` XDM-fältet, inklusive fälten `id`, `scope` och `scopeDetails` från förslagen.

Dessutom ställer du in fältet `include _experience.decisioning.propositionEventType.display` på `1`.
