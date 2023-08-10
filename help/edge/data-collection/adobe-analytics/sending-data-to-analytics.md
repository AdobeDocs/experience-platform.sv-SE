---
title: Skicka data till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig skicka data till Adobe Analytics med Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Skicka data till Adobe Analytics

Tidigare fanns det olika funktioner för att skilja mellan en sidvy och en länk (till exempel `s.t(), s.tl()`) finns det bara `sendEvent` -kommando. De data du skickar med en händelse avgör om det ska vara en sidvy eller en länk. [Läs mer om att spåra länkar](../track-links.md).

## Skicka en sidvy

Du kan ange en sidvy genom att ange `web.webPageDetails.pageViews.value=1` variabel.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Även om Analytics tekniskt sett registrerar en sidvy även om variabeln inte är inställd, är det en bra rutin att ställa in variabeln när du vill registrera en sidvy som explicit i dina data och att i framtiden kontrollera implementeringen.
