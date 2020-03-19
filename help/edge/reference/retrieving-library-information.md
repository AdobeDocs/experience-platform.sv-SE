---
title: Hämtar biblioteksinformation
seo-title: Hämta biblioteksinformation med Adobe Experience Platform Web SDK
description: Lär dig hur du hämtar information om det bibliotek som läses in på webbplatsen
seo-description: Lär dig hur du hämtar information om biblioteket som har lästs in på webbplatsen av Adobe Experience Cloud SDK samlar in automatiskt
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Hämtar biblioteksinformation

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK är för närvarande en betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Det är ofta praktiskt att komma åt en del av informationen bakom biblioteket som du har laddat in på din webbplats. Om du vill göra det kör du `getLibraryInfo` kommandot enligt följande:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

För närvarande innehåller det angivna `libraryInfo` objektet följande egenskaper:

* `version` Det här är versionen av det inlästa biblioteket. Om till exempel versionen av biblioteket som läses in är 1.0.0 blir värdet `1.0.0`.