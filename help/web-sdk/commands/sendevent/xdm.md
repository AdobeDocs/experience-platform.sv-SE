---
title: xdm
description: Lär dig hur du skickar data till Adobe via det schemajusterade XDM-objektet.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# `xdm`

The `xdm` -objektet innehåller datanyttolasten som skickas till Adobe. Fält som anges i det här objektet mappas direkt till element som definieras i datasetens schema.

Adobe Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Det här objektet har en maxgräns på 32 kB.

## Konfigurera XDM-objektet med Web SDK-tillägget

Ange **[!UICONTROL XDM]** -objekt inom åtgärderna för en taggregel. The [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) har ett intuitivt gränssnitt för att mappa andra dataelement till sina respektive XDM-fält.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Ange det dataelement som innehåller det önskade objektet i **[!UICONTROL XDM]** fält.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Konfigurera XDM-objektet med JavaScript-biblioteket för Web SDK

Ange `xdm` -objektet när `sendEvent` -kommando. Kontrollera att hierarkin i det här objektet matchar schemat för den konfigurerade datauppsättningen. Du kan inkludera båda `xdm` -objektet och [`data`](data.md) objekt i samma `sendEvent` -kommando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

I följande exempel används [Schemafältgrupp för Commerce Details](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```
