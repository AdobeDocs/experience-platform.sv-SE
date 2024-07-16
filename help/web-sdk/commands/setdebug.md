---
title: setDebug
description: Aktivera eller inaktivera felsökningsinställningen för Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Med kommandot `setDebug` kan du gå in i eller avsluta felsökningsläget i Web SDK. Det är ett av flera tillgängliga alternativ för [felsökning](../use-cases/debugging.md). Adobe rekommenderar att felsökningsläget aktiveras i utvecklingsmiljöer eller bara på din lokala dator i produktionsmiljöer.

## Ange felsökning med taggtillägget Web SDK

Med taggtillägget går det inte att växla felsökningsalternativ i användargränssnittet. Du kan antingen använda den anpassade kodredigeraren med JavaScript-syntax eller ange JavaScript-koden i webbläsarkonsolen när du befinner dig på webbplatsen.

## Ange felsökning med hjälp av JavaScript-biblioteket för Web SDK

Kör kommandot `setDebug` när du anropar den konfigurerade instansen av Web SDK. Det enda alternativet i konfigurationsobjektet är `enabled`, som är ett booleskt värde som avgör om felsökningsläget är aktiverat.

```js
alloy("setDebug", {"enabled": true});
```
