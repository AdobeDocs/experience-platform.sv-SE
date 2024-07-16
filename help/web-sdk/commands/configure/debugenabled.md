---
title: debugEnabled
description: Använd kod för att aktivera felsökningsfunktioner i Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

Med egenskapen `debugEnabled` kan du aktivera eller inaktivera felsökning med Web SDK-kod. Det är ett av de tillgängliga sätten att aktivera [felsökning](../../use-cases/debugging.md). Det kan vara lättare att aktivera felsökning i implementeringen än andra metoder vid webbplatsutveckling när du alltid vill ha felsökning aktiverat. Den här felsökningsmetoden gör att den kan användas av alla besökare, så den rekommenderas inte för produktionssidor.

På sidan [Felsökning](../../use-cases/debugging.md) finns fler sätt att aktivera felsökning.

## Aktivera felsökning med taggtillägget Web SDK

Det finns inga felsökningsalternativ som är tillgängliga internt med taggtillägget Web SDK. Använd en [alternativ felsökningsmetod](../../use-cases/debugging.md).

## Aktivera felsökning med Web SDK JavaScript-biblioteket

Ställ in det booleska värdet `debugEnabled` till `true` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
