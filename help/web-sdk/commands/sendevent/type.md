---
title: eventType
description: Ange händelsetypen för ett sendEvent-anrop.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# `eventType`

Med egenskapen `eventType` kan du definiera den typ av händelse som du skickar med Web SDK. Det här fältet fyller slutligen i fältet `xdm.eventType`. Det är värdefullt när du vill differentiera de händelsetyper som du skickar till Adobe.

Adobe innehåller vissa fördefinierade händelsetyper som du kan använda. En fullständig lista över fördefinierade värden finns i [Tillgängliga värden för `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) i användarhandboken för XDM. Du kan också använda dina egna värden om du vill.

Om du anger både `type` här och `xdm.eventType` i objektet [`xdm`](xdm.md) får värdet i det här fältet prioritet.

## Konfigurera händelsetyp med hjälp av taggtillägget Web SDK

Ange listrutefältet **[!UICONTROL Type]** i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Använd listrutan under fältet **[!UICONTROL Type]** eller ange ett eget värde.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Konfigurera händelsetyp med Web SDK JavaScript-biblioteket

Ange strängegenskapen `eventType` när du kör kommandot `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
