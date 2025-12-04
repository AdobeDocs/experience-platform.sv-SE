---
title: loggare
description: Utdata till webbläsarkonsolen vid felsökning.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# `logger`

Objektet `_satellite.logger` innehåller metoder som gör att du kan skicka diagnostikmeddelanden eller informationsmeddelanden till webbläsarkonsolen när [Felsökning](../use-cases/debugging.md) är aktiverat. Om felsökning inte är aktiverat gör alla `logger`-metodanrop ingenting.

Med dessa metoder kan utvecklare, teknikmarknadsförare och testare enkelt se vilka utlösare som finns i en taggegenskap och när. Eftersom dessa konsolmeddelanden endast visas när felsökning är aktiverat kan du lämna `logger` meddelanden i distributioner till produktionen utan att påverka webbläsarkonsolen för besökare på platsen.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Tidigare versioner av taggobjektet använde `_satellite.notify()`. Funktionen `notify()` är ersatt med `_satellite.logger`.

## Metoder

Alla `_satellite.logger`-metoder skickas till motsvarande JavaScript `console.*`-metod när felsökning är aktiverat. De flesta `console` argument eller objekt stöds med `_satellite.logger`:

| Metod | Vidarebefordrar till | Rekommenderade användningsområden |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Utförlig diagnostik. Vissa webbläsare kan behöva omfattande loggning för att kunna se den. |
| `_satellite.logger.log()` | `console.log()` | Allmänna meddelanden. |
| `_satellite.logger.info()` | `console.info()` | Informationshändelser på hög nivå. |
| `_satellite.logger.warn()` | `console.warn()` | Återställningsbara problem. Konsolposten är markerad som gul. |
| `_satellite.logger.error()` | `console.error()` | Fel. Konsolposten är röd. Adobe rekommenderar att du använder `error`-objekt för högar. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Konsolutdata

Biblioteket innehåller följande inställningar för alla konsolutdatameddelanden:

* **🚀**: Hjälper dig att enkelt identifiera vilka konsolmeddelanden som kommer från din taggimplementering.
* **\[Ursprung\]**: Namnet på regeln, åtgärden, tillägget eller dataelementet som loggen härstammar från. Om du anropar en loggningsmetod utanför implementeringen (till exempel via webbläsarkonsolen) används `[Custom Script]`.
* **Meddelandeutdata**: Meddelandeutdata inkluderas när metoden anropas.

>[!NOTE]
>
>Token för webbläsarformatering som `%c`, `%s` och `%d` används inte eftersom loggaren använder prefixet `🚀 [Origin]`.
