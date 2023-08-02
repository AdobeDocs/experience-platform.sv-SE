---
title: Spåra länkar med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: edf33d0d5991aed5c0535d0e7010aef082bcf48a
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Spåra länkar

Länkar kan anges manuellt eller spåras [automatiskt](#automaticLinkTracking). Manuell spårning görs genom att informationen läggs till under `web.webInteraction` del av schemat. Det finns två obligatoriska variabler:

* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

Från och med version 2.15.0 hämtar Web SDK `region` för det klickade HTML-elementet. Detta aktiverar [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) rapportfunktioner i Adobe Analytics.

Länktypen kan vara ett av tre värden:

* **`other`:** En anpassad länk
* **`download`:** En nedladdningslänk
* **`exit`:** En avslutningslänk

Dessa värden är [automatiskt mappad](adobe-analytics/automatically-mapped-vars.md) till Adobe Analytics om [konfigurerad](adobe-analytics/analytics-overview.md) att göra det.

## Automatisk länkspårning {#automaticLinkTracking}

Som standard hämtar, etiketterar och spelar Web SDK-filen in klick på kvalificerande länktaggar. Klickningar fångas med en [hämtning](https://www.w3.org/TR/uievents/#capture-phase) klicka på händelseavlyssnaren som är kopplad till dokumentet.

Automatisk länkspårning kan inaktiveras av [konfigurera](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK.

```javascript
clickCollectionEnabled: false
```

### Vilka taggar berättigar till länkspårning?{#qualifyingLinks}

Automatisk länkspårning utförs för ankarpunkter `A` och `AREA` -taggar. Dessa taggar beaktas dock inte för länkspårning om de har en bifogad `onclick` hanterare.

### Hur märks länkar?{#labelingLinks}

Länkarna är märkta som en nedladdningslänk om ankartaggen innehåller ett nedladdningsattribut eller om länken avslutas med ett populärt filtillägg. Hämtningslänkens kvalificerare kan vara [konfigurerad](../fundamentals/configuring-the-sdk.md) med reguljära uttryck:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Länkarna markeras som en avslutningslänk om länkens måldomän skiljer sig från den aktuella `window.location.hostname`.

Länkar som inte är kvalificerade som nedladdnings- eller avslutningslänk är märkta som &quot;other&quot;.

### Hur kan länkspårningsvärden filtreras?

De data som samlas in med automatisk länkspårning kan inspekteras och filtreras genom att en [callback-funktionen onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Det kan vara praktiskt att filtrera länkspårningsdata när data förbereds för analysrapporter. Automatisk länkspårning fångar både länkens namn och länkens URL. I analysrapporter har länknamnet prioritet framför länkens URL. Om du vill rapportera länkens URL måste länknamnet tas bort. I följande exempel visas en `onBeforeEventSend` funktion som tar bort länknamnet för nedladdningslänkar:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

Från och med Web SDK version 2.15.0 kan data som samlas in med automatisk länkspårning inspekteras, utökas eller filtreras genom att en [callback-funktionen onBeforeLinkClickSend](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Den här återanropsfunktionen körs bara när en automatisk länkklickningshändelse inträffar.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

När länkspårningshändelser filtreras med `onBeforeLinkClickSend` kommando, Adobe rekommenderar att du returnerar `false` för länkklickningar som inte ska spåras. Alla andra svar får Web SDK att skicka data till Edge Network.


>[!NOTE]
>
>** När båda `onBeforeEventSend` och `onBeforeLinkClickSend` återanropsfunktionerna är inställda, så kör Web SDK `onBeforeLinkClickSend` callback-funktionen för att filtrera och utöka interaktionshändelsen för länkklickning, följt av `onBeforeEventSend` callback-funktion.