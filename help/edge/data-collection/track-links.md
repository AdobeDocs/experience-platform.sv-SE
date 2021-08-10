---
title: Spåra länkar med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: d6460e442a136bf9bd26582f228017a6fb52138c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Spåra länkar

Länkar kan anges manuellt eller spåras [automatiskt](#automaticLinkTracking). Manuell spårning görs genom att informationen läggs till under `web.webInteraction`-delen av schemat. Det finns tre obligatoriska variabler:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        }
      },
      "name": "My Custom Link", // Name that shows up in the custom links report
      "URL": "https://myurl.com", // The URL of the link
      "type": "other" // values: other, download, exit
    }
  }
});
```

Länktypen kan vara ett av tre värden:

* **`other`:** En anpassad länk
* **`download`:** En nedladdningslänk
* **`exit`:** En avslutningslänk

Dessa värden [mappas automatiskt](adobe-analytics/automatically-mapped-vars.md) till Adobe Analytics om [konfigureras](adobe-analytics/analytics-overview.md) för att göra det.

## Automatisk länkspårning {#automaticLinkTracking}

Som standard hämtar, etiketterar och spelar Web SDK-filen in klick på kvalificerande länktaggar. Klickningar hämtas med en [klickningshändelseavlyssnare för klickning](https://www.w3.org/TR/uievents/#capture-phase) som är kopplad till dokumentet.

Automatisk länkspårning kan inaktiveras genom att [konfigurera](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK.

```javascript
clickCollectionEnabled: false
```

### Vilka taggar berättigar till länkspårning?{#qualifyingLinks}

Automatisk länkspårning utförs för taggarna `A` och `AREA`. Dessa taggar beaktas dock inte för länkspårning om de har en kopplad `onclick`-hanterare.

### Hur märks länkar?{#labelingLinks}

Länkarna är märkta som en nedladdningslänk om ankartaggen innehåller ett nedladdningsattribut eller om länken avslutas med ett populärt filtillägg. Hämtningslänkens kvalificerare kan vara [konfigurerad](../fundamentals/configuring-the-sdk.md) med ett reguljärt uttryck:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Länkarna markeras som en avslutningslänk om länkmåldomänen skiljer sig från den aktuella `window.location.hostname`.

Länkar som inte är kvalificerade som nedladdnings- eller avslutningslänk är märkta som &quot;other&quot;.

### Hur kan länkspårningsvärden filtreras?

Data som samlas in med automatisk länkspårning kan inspekteras och filtreras genom att en [onBeforeEventSend-återanropsfunktion](../fundamentals/tracking-events.md#modifying-events-globally) tillhandahålls.

Det kan vara praktiskt att filtrera länkspårningsdata när data förbereds för analysrapporter. Automatisk länkspårning fångar både länkens namn och länkens URL. I analysrapporter har länknamnet prioritet framför länkens URL. Om du vill rapportera länkens URL måste länknamnet tas bort. I följande exempel visas en `onBeforeEventSend`-funktion som tar bort länknamnet för nedladdningslänkar:

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

