---
title: getLibraryInfo
description: Hämta information om den aktuella Web SDK-biblioteksversionen.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

Kommandot `getLibraryInfo` ger dig information om vilken version av Web SDK-biblioteket som används. Du kan använda det här kommandot för att spåra vilka versioner av Web SDK som du distribuerar till olika webbegenskaper.

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

## Biblioteksinformation med hjälp av taggtillägget Web SDK

Taggtillägget har inget gränssnitt för att skicka det här kommandot. Använd den anpassade kodredigeraren enligt JavaScript bibliotekssyntax.

Om du kör det här kommandot med taggtillägget inkluderas både taggtilläggets version och biblioteksversionen, sammanfogade med en `+`-symbol. Web SDK Library-versionen visas först, följt av taggtilläggets version.
