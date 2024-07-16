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
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Objektet `turbine` är en&quot;kostnadsfri variabel&quot; inom omfånget för tilläggets biblioteksmoduler. Den innehåller information och verktyg som är specifika för tagghanteringen i Adobe Experience Platform och är alltid tillgänglig för biblioteksmoduler utan att använda `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` är ett objekt som innehåller bygginformation om det aktuella biblioteket för tagg-körning.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `turbineVersion` | Den [turbinversion](https://www.npmjs.com/package/@adobe/reactor-turbine) som används i det aktuella biblioteket. |
| `turbineBuildDate` | ISO 8601-datumet när versionen av [turbin](https://www.npmjs.com/package/@adobe/reactor-turbine) som används i behållaren skapades. |
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
| `stage` | Den miljö som det här biblioteket skapades för. Möjliga värden är `development`, `staging` och `production`. |

{style="table-layout:auto"}

## `debugEnabled`

Ett booleskt värde som anger om taggfelsökning är aktiverat.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. I stället loggar du alltid meddelanden med `turbine.logger` för att försäkra dig om att dina meddelanden bara skrivs ut till konsolen när taggfelsökning är aktiverat.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Returnerar värdet för ett dataelement.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Returnerar inställningsobjektet som senast sparades från vyn [tilläggskonfiguration](./configuration.md).

Observera att värden inom de returnerade inställningsobjekten kan komma från dataelement. Därför kan anrop av `getExtensionSettings()` vid olika tillfällen ge olika resultat om dataelementens värden har ändrats. Om du vill hämta de senaste värdena väntar du så länge som möjligt innan du anropar `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

Egenskapen [hostedLibFiles](./manifest.md) kan definieras inuti tilläggsmanifestet för att kunna lagra olika filer tillsammans med taggens körningsbibliotek. Den här modulen returnerar den URL där den angivna biblioteksfilen finns.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Hämtar en modul som har delats från ett annat tillägg. Om ingen matchande modul hittas returneras `undefined`. Mer information om delade moduler finns i [Implementera delade moduler](./web/shared.md).

## `logger`

```js
turbine.logger.error('Error!');
```

Loggningsverktyget används för att logga meddelanden till konsolen. Meddelanden visas bara i konsolen om användaren har aktiverat felsökning. Det rekommenderade sättet att aktivera felsökning är att använda [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob). Som ett alternativ kan användaren köra följande kommando `_satellite.setDebug(true)` i webbläsarens utvecklarkonsol. Loggaren har följande metoder:

* `logger.log(message: string)`: Loggar ett meddelande till konsolen.
* `logger.info(message: string)`: Loggar ett informationsmeddelande till konsolen.
* `logger.warn(message: string)`: Loggar ett varningsmeddelande till konsolen.
* `logger.error(message: string)`: Loggar ett felmeddelande till konsolen.
* `logger.debug(message: string)`: Loggar ett felsökningsmeddelande till konsolen. (Synligt bara när `verbose`-loggning är aktiverad i webbläsarkonsolen.)
* `logger.deprecation(message: string)`: Loggar ett varningsmeddelande till konsolen oavsett om taggfelsfunktionen är aktiverad av användaren eller inte.

## `onDebugChanged`

Genom att skicka en återanropsfunktion till `turbine.onDebugChanged` kommer taggarna att anropa återanropet när felsökningen är aktiverad. Taggar skickar ett booleskt värde till återanropsfunktionen som är true om felsökning var aktiverat eller false om felsökning var inaktiverad.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. I stället loggar du alltid meddelanden med `turbine.logger` och taggar så att dina meddelanden bara skrivs ut till konsolen när taggfelsfunktionen är aktiverad.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Ett objekt som innehåller följande inställningar som definieras av användaren för egenskapen i det aktuella taggredigeringsbiblioteket:

* `propertySettings.domains: Array<String>`

  En array med domäner som egenskapen omfattar.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  Tilläggsutvecklare bör inte bry sig om den här inställningen.
