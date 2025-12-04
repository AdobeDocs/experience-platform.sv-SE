---
title: renderDecision
description: Återge anpassat innehåll som är kvalificerat för automatisk återgivning.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

Med egenskapen `renderDecisions` kan du tvinga Web SDK att återge anpassat innehåll som kan återges automatiskt.

Ange det booleska värdet `renderDecisions` när du kör kommandot `sendEvent`. Om det utelämnas blir den här egenskapen som standard `false`. Ange den här egenskapen till `true` om du vill återge anpassat innehåll automatiskt.

>[!IMPORTANT]
>
>Egenskapen `renderDecisions` är inte kompatibel med egenskapen [`documentUnloading`](documentunloading.md). Undvik att ange båda egenskaperna till `true` samtidigt.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Kontrollera att du även inkluderar associerade omfattningar eller ytor när du anger den här egenskapen till `true`. Dessa omfattningar eller ytor kan begäras automatiskt (t.ex. på det första `sendEvent`-kommandot på en sida) eller explicit (med [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) eller [`personalization.surfaces`](personalization.md#personalizationsurfaces)). Ett vanligt problem vid återgivning av personalisering är följande:

1. Ett `sendEvent`-kommando körs tidigt på sidan som begär standardanpassning med `renderDecisions` inte inställt (standardvärdet är `false`). Fördrag hämtas men renderas inte.
1. Senare på sidan aktiveras en annan `sendEvent`-utlösare med `renderDecisions` inställt på `true`, men den innehåller inga omfång eller ytor. Eftersom det inte finns några scope eller ytor i det andra anropet återges ingenting.

Du kan undvika det här problemet genom att:

* Anger `renderDecisions` till `true` för det första `sendEvent` anropet, eller
* Anger `decisionScopes` eller `surfaces` explicit för ett efterföljande `sendEvent`-anrop när `renderDecisions` anges till `true`.

## Återge beslut med hjälp av taggtillägget Web SDK

SDK-taggtilläggets motsvarighet för den här egenskapen är kryssrutan [**Återge visuella personaliseringsbeslut**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) i åtgärden [!UICONTROL Send event].
