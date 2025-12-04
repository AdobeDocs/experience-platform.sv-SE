---
title: setDebug
description: Aktivera eller inaktivera felsökningsinställningen för Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

Med kommandot `setDebug` kan du gå in i eller avsluta felsökningsläget i Web SDK. Det är ett av flera tillgängliga alternativ för [felsökning](../../use-cases/debugging.md). Adobe rekommenderar att du aktiverar felsökningsläge i utvecklingsmiljöer eller bara på din lokala dator i produktionsmiljöer.

Kör kommandot `setDebug` när du anropar den konfigurerade instansen av Web SDK. Det enda alternativet i konfigurationsobjektet är `enabled`, som är ett booleskt värde som avgör om felsökningsläget är aktiverat.

```js
alloy("setDebug", {"enabled": true});
```

## Ange felsökning med taggtillägget Web SDK

Anropa [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) i webbläsarkonsolen på en sida där ett taggbibliotek implementeras. SDK-taggtillägget för webben erbjuder inte möjlighet att växla felsökningsalternativ i själva tagggränssnittet.
