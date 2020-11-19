---
title: Spårning av länkar med Adobe Analytics
seo-title: Länkspårning till Adobe Analytics med Adobe Experience Platform Web SDK
description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
seo-description: Lär dig hur du skickar länkdata till Adobe Analytics med Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Spåra länkar

Länkarna kan ställas in manuellt eller spåras [automatiskt](#automaticLinkTracking). Manuell spårning görs genom att informationen läggs till under `web.webInteraction` delen av schemat. Det finns tre obligatoriska variabler:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

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

## Automatisk länkspårning {#automaticLinkTracking}

Som standard hämtar, etiketterar och spelar Web SDK-filen in klick på kvalificerande länktaggar. Klickningar hämtas med en händelseavlyssnare för [klickning](https://www.w3.org/TR/uievents/#capture-phase) som bifogas till dokumentet.

Automatisk länkspårning kan inaktiveras genom att [konfigurera](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) Web SDK.

```javascript
clickCollectionEnabled: false
```

### Vilka taggar berättigar till länkspårning?{#qualifyingLinks}

Automatisk länkspårning utförs för ankarpunkter `A` och `AREA` taggar. Dessa taggar beaktas dock inte för länkspårning om de har en bifogad `onclick` hanterare.

### Hur märks länkar?{#labelingLinks}

Länkarna är märkta som en nedladdningslänk om ankartaggen innehåller ett nedladdningsattribut eller om länken avslutas med ett populärt filtillägg. Hämtningslänkens kvalificerare kan [konfigureras](../fundamentals/configuring-the-sdk.md) med ett reguljärt uttryck:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Länkarna markeras som en avslutningslänk om länkmåldomänen skiljer sig från den aktuella `window.location.hostname`.

Länkar som inte är kvalificerade som nedladdnings- eller avslutningslänk är märkta som &quot;other&quot;.
