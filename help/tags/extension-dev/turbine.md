---
title: Turbinfri variabel
description: Lär dig mer om turbinobjektet, en kostnadsfri variabel som ger information och verktyg som är specifika för tagghanteringen i Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Turbinfri variabel

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

The `turbine` är en&quot;kostnadsfri variabel&quot; inom omfånget för tilläggets biblioteksmoduler. Den innehåller information och verktyg som är specifika för tagghanteringen i Adobe Experience Platform och är alltid tillgänglig för biblioteksmoduler utan att använda `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` är ett objekt som innehåller bygginformation om det aktuella biblioteket för tagghantering.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `turbineVersion` | The [Turbin](https://www.npmjs.com/package/@adobe/reactor-turbine) version som används i det aktuella biblioteket. |
| `turbineBuildDate` | ISO 8601-datumet när versionen av [Turbin](https://www.npmjs.com/package/@adobe/reactor-turbine) som användes inuti behållaren skapades. |
| `buildDate` | ISO 8601-datumet när det aktuella biblioteket skapades. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` är ett objekt som innehåller information om miljön som biblioteket distribueras på.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | Miljöns ID. |
| `stage` | Den miljö som det här biblioteket skapades för. Möjliga värden är `development`, `staging`och `production`. |

{style="table-layout:auto"}

## `debugEnabled`

Ett booleskt värde som anger om taggfelsökning är aktiverat.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. Logga alltid meddelanden med `turbine.logger` för att vara säker på att dina meddelanden bara skrivs ut till konsolen när taggfelsfunktionen är aktiverad.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Returnerar värdet för ett dataelement.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Returnerar inställningsobjektet som senast sparades från [tilläggskonfiguration](./configuration.md) vy.

Observera att värden inom de returnerade inställningsobjekten kan komma från dataelement. På grund av detta, ringa `getExtensionSettings()` vid olika tidpunkter kan ge olika resultat om dataelementens värden har ändrats. Vänta så länge som möjligt innan du ringer för att få de senaste värdena `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

The [hostedLibFiles](./manifest.md) -egenskapen kan definieras inuti tilläggsmanifestet för att kunna lagra olika filer tillsammans med taggens körningsbibliotek. Den här modulen returnerar den URL där den angivna biblioteksfilen finns.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Hämtar en modul som har delats från ett annat tillägg. Om ingen matchande modul hittas `undefined` kommer att returneras. Se [Implementera delade moduler](./web/shared.md) om du vill ha mer information om delade moduler.

## `logger`

```js
turbine.logger.error('Error!');
```

Loggningsverktyget används för att logga meddelanden till konsolen. Meddelanden visas bara i konsolen om användaren har aktiverat felsökning. Det rekommenderade sättet att aktivera felsökning är att använda [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob). Användaren kan också köra följande kommando `_satellite.setDebug(true)` i webbläsarens utvecklarkonsol. Loggaren har följande metoder:

* `logger.log(message: string)`: Loggar ett meddelande till konsolen.
* `logger.info(message: string)`: Loggar ett informationsmeddelande till konsolen.
* `logger.warn(message: string)`: Loggar ett varningsmeddelande till konsolen.
* `logger.error(message: string)`: Loggar ett felmeddelande till konsolen.
* `logger.debug(message: string)`: Loggar ett felsökningsmeddelande till konsolen. (Synligt endast när `verbose` loggning är aktiverat i webbläsarkonsolen.)
* `logger.deprecation(message: string)`: Loggar ett varningsmeddelande till konsolen oavsett om taggfelsfunktionen är aktiverad av användaren eller inte.

## `onDebugChanged`

Genom att skicka en callback-funktion till `turbine.onDebugChanged`, kommer taggar att anropa återanropet när felsökning är aktiverat. Taggar skickar ett booleskt värde till återanropsfunktionen som är true om felsökning var aktiverat eller false om felsökning var inaktiverad.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. Logga alltid meddelanden med `turbine.logger` och taggarna ser till att dina meddelanden bara skrivs ut på konsolen när taggfelsfunktionen är aktiverad.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Ett objekt som innehåller följande inställningar som definieras av användaren för egenskapen i det aktuella taggredigeringsbiblioteket:

* `propertySettings.domains: Array<String>`

  En array med domäner som egenskapen omfattar.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  Tilläggsutvecklare bör inte bry sig om den här inställningen.
