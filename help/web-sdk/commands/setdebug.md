---
title: setDebug
description: Aktivera eller inaktivera felsökningsinställningen för Web SDK.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

The `setDebug` kan du gå in i eller avsluta felsökningsläget i Web SDK. Det är ett av flera alternativ för [felsökning](../use-cases/debugging.md). Adobe rekommenderar att felsökningsläget aktiveras i utvecklingsmiljöer eller bara på din lokala dator i produktionsmiljöer.

## Ange felsökning med taggtillägget Web SDK

Med taggtillägget går det inte att växla felsökningsalternativ i användargränssnittet. Du kan antingen använda den anpassade kodredigeraren med JavaScript-syntax eller ange JavaScript-koden i webbläsarkonsolen när du befinner dig på din plats.

## Ange felsökning med JavaScript-biblioteket för Web SDK

Kör `setDebug` när du anropar den konfigurerade instansen av Web SDK. Det enda alternativet i konfigurationsobjektet är `enabled`, som är ett booleskt värde som avgör om felsökningsläget är aktiverat.

```js
alloy("setDebug", {"enabled": true});
```
