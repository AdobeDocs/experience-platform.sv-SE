---
title: renderDecision
description: Återge anpassat innehåll som är kvalificerat för automatisk återgivning.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 1%

---

# `renderDecisions`

The `renderDecisions` Med -egenskapen kan du tvinga Web SDK att återge allt anpassat innehåll som kan återges automatiskt.

## Återge anpassat innehåll med hjälp av taggtillägget Web SDK

Välj **[!UICONTROL Render visual personalization decisions]** -kryssrutan i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Bläddra nedåt till [!UICONTROL Personalization] väljer du **[!UICONTROL Render visual personalization decisions]** kryssrutan.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Återge anpassat innehåll med JavaScript-biblioteket för Web SDK

Ange `renderDecisions` boolesk när `sendEvent` -kommando. Om det utelämnas blir den här egenskapen som standard `false`. Ange den här egenskapen som `true` om ni automatiskt vill återge personaliserat innehåll.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
