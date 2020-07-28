---
title: Hämtar biblioteksinformation
seo-title: Hämtar biblioteksinformation med Adobe Experience Platform Web SDK
description: Lär dig hur du hämtar information om det bibliotek som läses in på webbplatsen
seo-description: Lär dig hur du hämtar information om biblioteket som har lästs in på webbplatsen av Adobe Experience Cloud SDK samlar in automatiskt
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Hämtar biblioteksinformation

Det är ofta praktiskt att komma åt en del av informationen bakom biblioteket som du har laddat in på din webbplats. Om du vill göra det kör du `getLibraryInfo` kommandot enligt följande:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

För närvarande innehåller det angivna `libraryInfo` objektet följande egenskaper:

* `version` Det här är versionen av det inlästa biblioteket. Om till exempel versionen av biblioteket som läses in är 1.0.0 blir värdet `1.0.0`.