---
title: xdm
description: Lär dig hur du skickar data till Adobe via det schemajusterade XDM-objektet.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

Objektet `xdm` innehåller datanyttolasten som skickats till Adobe. Fält som anges i det här objektet mappas direkt till element som definieras i datasetens schema.

Adobe Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Ange objektet `xdm` när du kör kommandot `sendEvent`. Kontrollera att hierarkin i det här objektet matchar schemat för den konfigurerade datauppsättningen. Du kan inkludera både objektet `xdm` och objektet [`data`](data.md) i samma `sendEvent`-kommando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

I följande exempel används schemafältgruppen [Commerce Details](/help/xdm/field-groups/event/commerce-details.md):

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

## Använd objektet `xdm` med hjälp av taggtillägget Web SDK

Objektet `xdm` är antingen tillgängligt som ett [variabelt dataelement](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) eller [XDM-objektdataelement](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) när du använder taggtillägget för Web SDK. Adobe rekommenderar att du i de flesta fall använder ett variabelt dataelement.
