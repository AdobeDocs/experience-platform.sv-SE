---
title: documentUnloading
description: Använd JavaScript-API:t sendBeacon för att skicka data till Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# `documentUnloading`

The `documentUnloading` -egenskapen gör att du kan använda JavaScript [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) metod för att skicka data till Adobe. Om en vanlig begäran tar för lång tid kan webbläsaren avbryta den. Du kan ange att Web SDK ska använda `sendBeacon` så att begäran körs i bakgrunden när du navigerar bort från sidan. Aktivera den här egenskapen för att förhindra att dataförfrågningar avbryts av webbläsaren vid borttagning.

Flera webbläsare har en gräns på 64 kB för den mängd data som kan skickas med `sendBeacon` samtidigt. Om webbläsaren avvisar händelsen eftersom nyttolasten är för stor återgår Web SDK till sin normala transportmetod.

## Konfigurera dokumentborttagning med hjälp av taggtillägget Web SDK

Aktivera **[!UICONTROL Document will unload]** -kryssrutan i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Aktivera **[!UICONTROL Document will unload]** kryssrutan i [!UICONTROL Data] -avsnitt.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Konfigurera dokumentborttagning med JavaScript-biblioteket för Web SDK

Ange `documentUnloading` boolesk när `sendEvent` -kommando. Standardvärdet är `false`. Ange den här egenskapen som `true` om du vill använda `sendBeacon` metod för att skicka data till Adobe.

>[!IMPORTANT]
>
>The `documentUnloading` egenskapen är inte kompatibel med [`renderDecisions`](renderdecisions.md) -egenskap. Du bör inte ange båda egenskaperna till `true` samtidigt.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
