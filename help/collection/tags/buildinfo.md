---
title: buildInfo
description: Hämta information om taggbygget som implementerats på din webbplats.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 2%

---

# `buildInfo`

Objektet `_satellite.buildInfo` innehåller information om hur taggegenskapen byggs. Det här objektet är mest användbart vid felsökning av ofta förekommande byggen för att säkerställa att du använder den senaste versionen.

```ts
readonly _satellite.buildInfo: BuildInfo
```

## Tillgängliga fält

Följande fält är tillgängliga när det här objektet anropas.

```json
{
  "minified": true,
  "buildDate": "YYYY-06-13T01:22:12Z",
  "turbineBuildDate": "YYYY-08-22T17:32:44Z",
  "turbineVersion": "28.0.0"
}
```

| Namn | Typ | Beskrivning |
| --- | --- | --- |
| **`minified`** | `boolean` | Anger om biblioteket är minifierat. Produktionsbyggen är vanligtvis minifierade (`true`), medan utvecklings- och mellanlagringsbyggen vanligtvis inte är det (`false`). |
| **`buildDate`** | `string (ISO-8601 datetime)` | Datum och tid då JavaScript-filen skapades och publicerades. |
| **`turbineBuildDate`** | `string (ISO-8601 datetime)` | [Turbinen](https://github.com/adobe/reactor-turbine) är en Adobe-motor som bearbetar taggregler och delegerar logik för att tagga tillägg. Det här fältet innehåller datum och tid för turbinbygget som används för att publicera taggegenskapen. |
| **`turbineVersion`** | `string` | Den version av Turbine som användes för att skapa och publicera taggegenskapen. |

Liknande information finns också i `_satellite._container.buildInfo`. Mer information finns i [`_container`](container.md).
