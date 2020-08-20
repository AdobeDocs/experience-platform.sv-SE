---
title: Hämtar biblioteksinformation
seo-title: Hämta biblioteksinformation med Adobe Experience Platform Web SDK
description: Lär dig hur du hämtar information om det bibliotek som läses in på webbplatsen
seo-description: Lär dig hur du hämtar information om biblioteket som har lästs in på webbplatsen av Adobe Experience Cloud SDK samlar in automatiskt
keywords: library; library information;getLibraryInfo;libraryInfo;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
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