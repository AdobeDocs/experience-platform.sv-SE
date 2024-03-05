---
title: debugEnabled
description: Använd kod för att aktivera felsökningsfunktioner i Web SDK.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

The `debugEnabled` kan du aktivera eller inaktivera felsökning med Web SDK-kod. Det är ett av de tillgängliga sätten att aktivera [felsökning](../../use-cases/debugging.md). Det kan vara lättare att aktivera felsökning i implementeringen än andra metoder vid webbplatsutveckling när du alltid vill ha felsökning aktiverat. Den här felsökningsmetoden gör att den kan användas av alla besökare, så den rekommenderas inte för produktionssidor.

Se [Felsökning](../../use-cases/debugging.md) använd fallsida om du vill ha fler sätt att aktivera felsökning.

## Aktivera felsökning med taggtillägget Web SDK

Det finns inga felsökningsalternativ som är tillgängliga internt med taggtillägget Web SDK. Använd en [alternativ felsökningsmetod](../../use-cases/debugging.md).

## Aktivera felsökning med JavaScript-biblioteket för Web SDK

Ange `debugEnabled` boolesk till `true` när du kör `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
