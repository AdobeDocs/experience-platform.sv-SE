---
title: konversation
description: Konfigurera inställningar för Brand Concierge-chatt.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge för webben: SDK är för närvarande i **beta**. Funktionen och dokumentationen kan komma att ändras.

Objektet `conversation` innehåller konfigurationsalternativ för Brand Concierge chattsessioner. Det här objektet stöds i Web SDK version 2.31.0 eller senare.

## Egenskaper

| Egenskap | Typ | Beskrivning |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Avgör om Web SDK läser frågesträngsparametern `adobe_brand_concierge_source` och inkluderar den i `xdm.channel.referringSource`. Standardvärdet är `false`. |
| **`stickyConversationSession`** | `boolean` | Avgör om Web SDK anger en sessionscookie för att bevara Brand Concierge chattsessioner över sidinläsningar. Standardvärdet är `false`. Om det utelämnas eller anges till `false` startar Brand Concierge-chatten en ny session vid varje sidinläsning. |

## Exempel

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## Konfigurera konversationsinställningar med hjälp av taggtillägget Web SDK

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med [Brand Concierge-inställningar](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
