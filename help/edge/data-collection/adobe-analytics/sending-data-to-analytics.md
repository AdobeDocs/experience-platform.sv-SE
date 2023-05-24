---
title: Skicka data till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar data till Adobe Analytics med Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
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
