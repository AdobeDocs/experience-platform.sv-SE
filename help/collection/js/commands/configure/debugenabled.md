---
title: debugEnabled
description: Använd kod för att aktivera felsökningsfunktioner i Web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

Med egenskapen `debugEnabled` kan du aktivera eller inaktivera felsökning med Web SDK-kod. Det är ett av de tillgängliga sätten att aktivera [felsökning](/help/collection/use-cases/debugging.md). Det kan vara lättare att aktivera felsökning i implementeringen än andra metoder vid webbplatsutveckling när du alltid vill ha felsökning aktiverat. Den här felsökningsmetoden gör att den kan användas av alla besökare, så den rekommenderas inte för produktionssidor. På sidan [Felsökning](/help/collection/use-cases/debugging.md) finns fler sätt att aktivera felsökning.

Ställ in det booleska värdet `debugEnabled` till `true` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `false`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Aktivera felsökning med taggtillägget Web SDK

Det finns inga felsökningsalternativ som är tillgängliga i SDK-taggtillägget för webben. Använd en [alternativ felsökningsmetod](/help/collection/use-cases/debugging.md) när du konfigurerar taggegenskapen.
