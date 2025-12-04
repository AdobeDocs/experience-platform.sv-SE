---
title: eventType
description: Ange händelsetypen för ett sendEvent-anrop.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

Med egenskapen `eventType` kan du definiera den typ av händelse som du skickar med Web SDK. Det här fältet fyller slutligen i fältet `xdm.eventType`. Det är värdefullt när du vill differentiera de händelsetyper som du skickar till Adobe.

Adobe innehåller vissa fördefinierade händelsetyper som du kan använda. En fullständig lista över fördefinierade värden finns i [Tillgängliga värden för `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) i användarhandboken för XDM. Du kan också använda dina egna värden om du vill.

Om du anger både `type` här och `xdm.eventType` i objektet [`xdm`](xdm.md) får värdet i det här fältet prioritet.

Ange strängegenskapen `eventType` när du kör kommandot `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Händelsetyp som använder taggtillägget Web SDK

SDK-taggtillägget för webben för den här egenskapen är den nedrullningsbara menyn [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) när en [!UICONTROL Send event]-åtgärd konfigureras.
