---
title: getLibraryInfo
description: Hämta information om den aktuella Web SDK-biblioteksversionen.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

Kommandot `getLibraryInfo` ger dig information om vilken version av Web SDK-biblioteket som används. Du kan använda det här kommandot för att spåra vilka versioner av Web SDK som du distribuerar till olika webbegenskaper.

## Biblioteksinformation med hjälp av taggtillägget Web SDK

Taggtillägget har inget gränssnitt för att skicka det här kommandot. Använd den anpassade kodredigeraren enligt JavaScript bibliotekssyntax.

Om du kör det här kommandot med taggtillägget inkluderas både taggtilläggets version och biblioteksversionen, sammanfogade med en `+`-symbol. Web SDK-biblioteksversionen visas först, följt av taggtilläggets version.

## Biblioteksinformation med hjälp av JavaScript-biblioteket för Web SDK

Kör kommandot `getLibraryInfo` när du anropar den konfigurerade instansen av Web SDK. Det här kommandot är vanligtvis parat med ett JavaScript-löfte som gör att du kan hämta de objekt som det fyller i.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Svarsobjekt

Om du bestämmer dig för att [hantera svar](command-responses.md) med det här kommandot är följande egenskaper tillgängliga i svarsobjektet:

* **`libraryInfo.commands`**: En array med kommandon som stöds i den här versionen av Web SDK.
* **`libraryInfo.configs`**: En matris med konfigurationsinställningar som stöds i den här versionen av Web SDK.
* **`libraryInfo.version`**: Versionen av Web SDK-biblioteket.
