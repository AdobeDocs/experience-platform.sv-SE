---
title: Hantera webbhändelser i SDK
description: Beskriver vad displayhändelser är och hur du kan använda dem i Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Hantera webbhändelser i SDK

Webbhändelser används av Web SDK för att informera din personaliserings- eller analystjänst när ett visst personaliseringsinnehåll visas på en sida. Genom att skicka visningshändelser förbättras noggrannheten i mätvärdena för personalisering och du får en korrekt översikt över vad användarna ser på sidan.

>[!NOTE]
>
>Visningshändelser skickas inte automatiskt när funktionen `applyPropositions` anropas.

## Skicka visningshändelser automatiskt

När du skickar visningshändelser får du automatiskt mer korrekta analysmått, eftersom händelsen skickas omedelbart efter att personaliseringen har lästs in. Den här implementeringen har också en effektivare implementeringsmetod.

Om du vill skicka visningshändelser automatiskt när det anpassade innehållet återges på sidan måste du konfigurera följande parametrar:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` eller inte angivet

Web SDK skickar visningshändelserna omedelbart efter att någon personalisering har renderats som ett resultat av ett `sendEvent`-anrop.

## Skicka visningshändelser i efterföljande sendEvent-anrop

Jämfört med att automatiskt skicka visningshändelser kan du även inkludera mer information om sidinläsningen i anropet när du inkluderar dem i efterföljande `sendEvent` samtal. Det kan vara extra information som inte var tillgänglig när det personliga innehållet begärdes.

Om du skickar visningshändelser i `sendEvent` anrop minimeras dessutom avhoppsfrekvensen när du använder Adobe Analytics.

>[!IMPORTANT]
>
>När du använder manuellt återgivna profiler stöds endast visningshändelser via `sendEvent` anrop. I det här fallet kan du inte skicka visningshändelser automatiskt.

### Skicka visningshändelser för automatiskt återgivna förslag

Om du vill skicka visningshändelser för automatiskt återgivna profiler måste du konfigurera följande parametrar i `sendEvent`-anropet:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` för sidträffens överkant

Om du vill skicka visningshändelser anropar du `sendEvent` med `personalization.includeRenderedPropositions: true`

### Skicka visningshändelser för manuellt återgivna förslag

Om du vill skicka visningshändelser för manuellt återgivna utkast måste du inkludera dem i `_experience.decisioning.propositions` XDM-fältet, inklusive fälten `id`, `scope` och `scopeDetails` från förslagen.

Dessutom ställer du in fältet `include _experience.decisioning.propositionEventType.display` på `1`.
