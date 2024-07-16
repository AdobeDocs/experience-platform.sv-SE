---
title: documentUnloading
description: Använd JavaScript sendBeacon API för att skicka data till Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# `documentUnloading`

Med egenskapen `documentUnloading` kan du använda JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)-metoden för att skicka data till Adobe. Om en vanlig begäran tar för lång tid kan webbläsaren avbryta den. Du kan ange att Web SDK ska använda `sendBeacon` så att begäran körs i bakgrunden när du navigerar bort från sidan. Aktivera den här egenskapen för att förhindra att dataförfrågningar avbryts av webbläsaren vid borttagning.

Flera webbläsare har en gräns på 64 kB för den mängd data som kan skickas med `sendBeacon` samtidigt. Om webbläsaren avvisar händelsen eftersom nyttolasten är för stor återgår Web SDK till sin normala transportmetod.

## Konfigurera dokumentborttagning med hjälp av taggtillägget Web SDK

Aktivera kryssrutan **[!UICONTROL Document will unload]** i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Aktivera kryssrutan **[!UICONTROL Document will unload]** i avsnittet [!UICONTROL Data].
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Konfigurera dokumentborttagning med hjälp av JavaScript-biblioteket för Web SDK

Ange det booleska värdet `documentUnloading` när du kör kommandot `sendEvent`. Dess standardvärde är `false`. Ange den här egenskapen till `true` om du vill använda metoden `sendBeacon` för att skicka data till Adobe.

>[!IMPORTANT]
>
>Egenskapen `documentUnloading` är inte kompatibel med egenskapen [`renderDecisions`](renderdecisions.md). Du bör inte ange båda egenskaperna till `true` samtidigt.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
