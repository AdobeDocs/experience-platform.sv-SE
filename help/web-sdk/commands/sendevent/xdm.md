---
title: xdm
description: Det schemajusterade objekt som skickas till Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# `xdm`

The `xdm` -objektet innehåller datanyttolasten som skickas till Adobe. Fält som anges i det här objektet mappas direkt till element som definieras i datasetens schema.

Adobe Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Det här fältet har en maxgräns på 32 kB.

## Konfigurera XDM-objektet med Web SDK-tillägget

Ange **[!UICONTROL XDM]** -fält inom åtgärderna för en taggregel. The [XDM-objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) har ett intuitivt gränssnitt för att mappa andra dataelement till sina respektive XDM-fält.

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

I följande exempel används [Schemafältgrupp för handelsinformation](/help/xdm/field-groups/event/commerce-details.md):

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
