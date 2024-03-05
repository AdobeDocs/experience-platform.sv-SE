---
title: getLibraryInfo
description: Hämta information om den aktuella Web SDK-biblioteksversionen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

The `getLibraryInfo` innehåller information om den version av Web SDK-biblioteket som används. Du kan använda det här kommandot för att spåra vilka versioner av Web SDK som du distribuerar till olika webbegenskaper.

## Biblioteksinformation med hjälp av taggtillägget Web SDK

Taggtillägget har inget gränssnitt för att skicka det här kommandot. Använd den anpassade kodredigeraren enligt JavaScript-bibliotekssyntaxen.

Om du kör det här kommandot med taggtillägget inkluderas både taggtilläggets version och biblioteksversionen, sammanfogade med en `+` symbol. Web SDK-biblioteksversionen visas först, följt av taggtilläggets version.

## Biblioteksinformation med hjälp av JavaScript-biblioteket för Web SDK

Kör `getLibraryInfo` när du anropar den konfigurerade instansen av Web SDK. Det här kommandot är vanligtvis parat med ett JavaScript-löfte som gör att du kan hämta de objekt som det fyller i.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Svarsobjekt

Om du väljer att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`libraryInfo.commands`**: En array med kommandon som stöds i den här versionen av Web SDK.
* **`libraryInfo.configs`**: En array med konfigurationsinställningar som stöds i den här versionen av Web SDK.
* **`libraryInfo.version`**: Versionen av Web SDK-biblioteket.
