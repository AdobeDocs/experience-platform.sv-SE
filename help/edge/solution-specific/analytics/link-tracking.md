---
title: Sid- och länkspårning med Adobe Analytics
seo-title: Länkspårning till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8840e00ec3aa28d43c371b793da4a4b9bfc8d259
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Skicka data till Adobe Analytics

Tidigare fanns det olika funktioner för att skilja mellan en sidvy och en länk (till exempel `s.t(), s.tl()`), men i Web SDK finns bara `sendEvent` kommandot. De data du skickar med en händelse avgör om det ska vara en sidvy eller en länk.

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

Även om analysfunktionen tekniskt sett registrerar en sidvy även om variabeln inte är inställd, är det bäst att ställa in variabeln när du vill registrera en sidvy som explicit i dina data och att i framtiden bevisa implementeringen.

## Spårningslänkar

Länkarna kan ställas in manuellt eller spåras [automatiskt](#automaticLinkTracking). Manuell spårning görs genom att informationen läggs till under `web.webInteraction` delen av schemat. Det finns tre obligatoriska variabler: `web.webInteraction.name`, `web.webInteraction.type` och `web.webInteraction.linkClicks.value`.

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
  }
});
```

Länktypen kan vara ett av tre värden:

* **`other`:** En anpassad länk
* **`download`:** En nedladdningslänk
* **`exit`:** En avslutningslänk

### Automatisk länkspårning {#automaticLinkTracking}

Som standard hämtar Web SDK, [etiketter](#labelingLinks)och [poster](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) klickar på [kvalificerande](#qualifyingLinks) länktaggar. Klickningar hämtas med en händelseavlyssnare för [klickning](https://www.w3.org/TR/uievents/#capture-phase) som bifogas till dokumentet.

Du kan inaktivera automatisk länkspårning genom att [konfigurera](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK.

```javascript
clickCollectionEnabled: false
```

#### Vilka taggar berättigar till länkspårning?{#qualifyingLinks}

Automatisk länkspårning utförs för ankarpunkter `A` och `AREA` taggar. Dessa taggar beaktas dock inte för länkspårning om de har en bifogad `onclick` hanterare.

#### Hur märks länkar?{#labelingLinks}

Länkarna är märkta som en nedladdningslänk om ankartaggen innehåller ett nedladdningsattribut eller om länken avslutas med ett populärt filtillägg. Hämtningslänkens kvalificerare kan [konfigureras](../../fundamentals/configuring-the-sdk.md) med ett reguljärt uttryck:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Länkarna markeras som en avslutningslänk om länkmåldomänen skiljer sig från den aktuella `window.location.hostname`.

Länkar som inte är kvalificerade som nedladdnings- eller avslutningslänk är märkta som &quot;other&quot;.
