---
title: eventType
description: Ange händelsetypen för ett sendEvent-anrop.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# `eventType`

The `eventType` kan du definiera vilken typ av händelse du skickar med Web SDK. Det här fältet fyller i `xdm.eventType` fält. Det är värdefullt när du vill differentiera de händelsetyper som du skickar till Adobe.

Adobe innehåller vissa fördefinierade händelsetyper som du kan använda. Se [Tillgängliga värden för `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) i användarhandboken för XDM om du vill se en fullständig lista över fördefinierade värden. Du kan också använda dina egna värden om du vill.

Om du anger båda `type` här och `xdm.eventType` i [`xdm`](xdm.md) -objekt får värdet i det här fältet prioritet.

## Konfigurera händelsetyp med hjälp av taggtillägget Web SDK

Ange **[!UICONTROL Type]** listrutefält inom åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Använd listrutan under **[!UICONTROL Type]** eller ange ett eget värde.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Konfigurera händelsetyp med JavaScript-biblioteket för Web SDK

Ange `eventType` string-egenskap när den körs `sendEvent` -kommando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
