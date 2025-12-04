---
title: documentUnloading
description: Använd JavaScript sendBeacon API för att skicka data till Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

Med egenskapen `documentUnloading` kan du använda JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)-metod för att skicka data till Adobe. Om en vanlig begäran tar för lång tid kan webbläsaren avbryta den. Du kan ange att Web SDK ska använda `sendBeacon` så att begäran körs i bakgrunden när du navigerar bort från sidan. Aktivera den här egenskapen för att förhindra att dataförfrågningar avbryts av webbläsaren vid borttagning.

Flera webbläsare har en gräns på 64 kB för den mängd data som kan skickas med `sendBeacon` samtidigt. Om webbläsaren avvisar händelsen på grund av att nyttolasten är för stor, använder Web SDK sin normala transportmetod. Även om en viss webbläsare tillåter större nyttolaster kortar Adobe datainsamlingsservrar av nyttolasterna ned till 64 kB.

Ange det booleska värdet `documentUnloading` när du kör kommandot `sendEvent`. Dess standardvärde är `false`. Ange den här egenskapen till `true` om du vill använda metoden `sendBeacon` för att skicka data till Adobe.

>[!IMPORTANT]
>
>Egenskapen `documentUnloading` är inte kompatibel med egenskapen [`renderDecisions`](renderdecisions.md). Undvik att ange båda egenskaperna till `true` samtidigt.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Ta bort dokument med taggtillägget Web SDK

Kryssrutan **[!UICONTROL Document will unload]** är tillgänglig när du konfigurerar en [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields)-åtgärd när du använder taggtillägget Web SDK.
