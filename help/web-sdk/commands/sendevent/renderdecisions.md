---
title: renderDecision
description: Återge anpassat innehåll som är kvalificerat för automatisk återgivning.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 1%

---

# `renderDecisions`

Med egenskapen `renderDecisions` kan du tvinga Web SDK att återge anpassat innehåll som kan återges automatiskt.

## Återge anpassat innehåll med hjälp av taggtillägget Web SDK

Markera kryssrutan **[!UICONTROL Render visual personalization decisions]** i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Bläddra ned till avsnittet [!UICONTROL Personalization] och markera kryssrutan **[!UICONTROL Render visual personalization decisions]**.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Återge personaliserat innehåll med hjälp av JavaScript-biblioteket för Web SDK

Ange det booleska värdet `renderDecisions` när du kör kommandot `sendEvent`. Om det utelämnas blir den här egenskapen som standard `false`. Ange den här egenskapen till `true` om du vill återge anpassat innehåll automatiskt.

>[!IMPORTANT]
>
>Egenskapen `renderDecisions` är inte kompatibel med egenskapen [`documentUnloading`](documentunloading.md). Du bör inte ange båda egenskaperna till `true` samtidigt.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
