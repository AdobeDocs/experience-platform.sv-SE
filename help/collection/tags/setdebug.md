---
title: setDebug()
description: Aktivera felsökning på webbplatsen via webbläsarkonsolen.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

Med metoden `_satellite.setDebug()` kan du aktivera eller inaktivera [Felsökning](../use-cases/debugging.md) på din plats. Den här metoden är avsedd att köras lokalt i webbläsarkonsolen. Adobe rekommenderar att du inte anropar den här metoden i taggregler.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: Aktiverar [felsökning](../use-cases/debugging.md). Meddelanden som genereras av taggbiblioteket (inklusive [`_satellite.logger`](logger.md)) visas i webbläsarkonsolen.
* **`_satellite.setDebug(false);`**: Inaktiverar felsökning. Konsolmeddelanden som genereras av taggbiblioteket visas inte.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>Meddelanden som skrivits med JavaScript inbyggt `console.log()` är alltid synliga för alla som har DevTools öppet. Adobe rekommenderar att du använder [`_satellite.logger`](logger.md) där det är möjligt.

## Felsökningslägesbeständighet

När du anropar den här metoden används följande omfång i felsökningsläget:

* **Webbläsarsession**: felsökningsläget kvarstår över sidinläsningar. Den är aktiverad tills du avslutar webbläsarsessionen eller uttryckligen inaktiverar den.
* **Ursprungligt omfång**: felsökningsläget kvarstår bara för samma plats (domän + port + protokoll).
* **Per webbläsarprofil**: felsökningsläget är inte korsprofil.

Andra former av [felsökning](../use-cases/debugging.md) kan påverka och skriva över felsökningsläget med hjälp av webbläsarkonsolmetoden.
