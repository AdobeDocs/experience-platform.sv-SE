---
title: Sid- och länkspårning med Adobe Analytics
seo-title: Länkspårning till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: c9d777f4350f0b039608c4f9b01d5206994e2572
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Skicka data till Adobe Analytics

Tidigare fanns det olika funktioner för att skilja mellan en sidvy och en länk (till exempel `s.t(), s.tl()`), men i Web SDK finns bara `sendEvent` kommandot. De data du skickar med en händelse avgör om det ska vara en sidvy eller en länk. [Läs mer om att spåra länkar](../track-links.md).

## Skicka en sidvy

Du kan ange en sidvy genom att ställa in `web.webPageDetails.pageViews.value=1` variabeln.

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
