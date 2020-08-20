---
title: Sid- och länkspårning med Adobe Analytics
seo-title: Länkspårning till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Skicka data till Adobe Analytics

Tidigare fanns det olika funktioner att skilja mellan en sidvy och en länk (till exempel `s.t(), s.tl()`), men i Web SDK finns bara `sendEvent` kommandot. De data du skickar med en händelse avgör om det ska vara en sidvy eller en länk.

## Skicka en sidvy

Du kan ange en sidvy genom att ställa in `web.webPageDetails.pageViews.value=1` variabeln.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Även om analysfunktionen tekniskt sett registrerar en sidvy även om variabeln inte är inställd, är det bäst att ställa in den här variabeln när du vill registrera en sidvy som explicit i dina data och att framtidskorrektur för implementeringen.

## Spårningslänkar

Länkar kan anges genom att informationen läggs till under `web.webInteraction` delen av schemat. Det finns tre obligatoriska variabler: `web.webInteraction.name`, `web.webInteraction.type` och `web.webInteraction.linkClicks.value`.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
    }
  }
});
```

Länktypen kan vara ett av tre värden:

* **`other`:** En anpassad länk
* **`download`:** En nedladdningslänk (dessa kan spåras automatiskt av biblioteket)
* **`exit`:** En avslutningslänk

### Automatisk länkspårning

Web SDK kan automatiskt spåra alla länkklick genom att aktivera [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

Hämtningslänkar identifieras automatiskt baserat på populära filtyper. Logiken för hur nedladdningar klassificeras är konfigurerbar.
