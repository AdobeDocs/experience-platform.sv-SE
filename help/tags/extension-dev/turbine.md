---
title: Turbinfri variabel
description: Lär dig mer om turbinobjektet, en kostnadsfri variabel som ger information och verktyg som är specifika för tagghanteringen i Adobe Experience Platform.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 57b4d11d0a7fd587dc45066737726a52533e33f0
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# Turbinfri variabel

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Objektet `turbine` är en &quot;fri variabel&quot; inom omfånget för tilläggets biblioteksmoduler. Den innehåller information och verktyg som är specifika för tagghanteringen i Adobe Experience Platform och är alltid tillgänglig för biblioteksmoduler utan att använda `require()`.

## [!DNL buildInfo]

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
| `turbineVersion` | Den [turbinversion](https://www.npmjs.com/package/@adobe/reactor-turbine) som används i det aktuella biblioteket. |
| `turbineBuildDate` | ISO 8601-datumet när den version av [turbin](https://www.npmjs.com/package/@adobe/reactor-turbine) som används inuti behållaren skapades. |
| `buildDate` | ISO 8601-datumet när det aktuella biblioteket skapades. |


## [!DNL environment]

```js
console.log(turbine.environment.stage);
```

`turbine.environment` är ett objekt som innehåller information om miljön som biblioteket distribueras på.

```js
{
    id: "EN123456...",
    stage: "development"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | ID för miljön. |
| `stage` | Den miljö som det här biblioteket skapades för. Godkända värden är `development`, `staging` och `production`. |


## [!DNL debugEnabled]

Om taggfelsökning är aktiverat.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. I stället loggar du alltid meddelanden med `turbine.logger` för att vara säker på att dina meddelanden bara skrivs ut till konsolen när taggfelsökning är aktiverat.

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Returnerar värdet för ett dataelement.

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Returnerar inställningsobjektet som senast sparades från vyn [tilläggskonfiguration](./configuration.md).

Observera att värden inom de returnerade inställningsobjekten kan komma från dataelement. Därför kan anrop till `getExtensionSettings()` vid olika tidpunkter ge olika resultat om dataelementens värden har ändrats. Om du vill få de senaste värdena väntar du så länge som möjligt innan du ringer `getExtensionSettings()`.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

Egenskapen [hostedLibFiles](./manifest.md) kan definieras inuti tilläggsmanifestet för att kunna vara värd för olika filer tillsammans med taggens körningsbibliotek. Den här modulen returnerar den URL där den angivna biblioteksfilen finns.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Hämtar en modul som har delats från ett annat tillägg. Om ingen matchande modul hittas returneras `undefined`. Mer information om delade moduler finns i [Implementera delade moduler](./web/shared.md).

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

Loggningsverktyget används för att logga meddelanden till konsolen. Meddelanden visas bara i konsolen om användaren har aktiverat felsökning. Det rekommenderade sättet att aktivera felsökning är att använda [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). Alternativt kan användaren köra följande kommando `_satellite.setDebug(true)` i webbläsarens utvecklarkonsol. Loggaren har följande metoder:

* `logger.log(message: string)`: Loggar ett meddelande till konsolen.
* `logger.info(message: string)`: Loggar ett informationsmeddelande till konsolen.
* `logger.warn(message: string)`: Loggar ett varningsmeddelande till konsolen.
* `logger.error(message: string)`: Loggar ett felmeddelande till konsolen.
* `logger.debug(message: string)`: Loggar ett felsökningsmeddelande till konsolen. (Synligt bara när `verbose`-loggning är aktiverad i webbläsarkonsolen.)

### [!DNL onDebugChanged]

Genom att skicka en återanropsfunktion till `turbine.onDebugChanged`, kommer taggarna att anropa återanropet när felsökningen är aktiverad. Taggar skickar ett booleskt värde till återanropsfunktionen som är true om felsökning var aktiverat eller false om felsökning var inaktiverad.

Om du bara försöker logga meddelanden är det osannolikt att du kommer att behöva använda detta. I stället loggar du alltid meddelanden med `turbine.logger` och -taggar så att dina meddelanden bara skrivs ut till konsolen när taggfelsökning är aktiverat.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Ett objekt som innehåller följande inställningar som definieras av användaren för egenskapen i det aktuella taggredigeringsbiblioteket:

* `propertySettings.domains: Array<String>`

   En array med domäner som egenskapen omfattar.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Tilläggsutvecklare bör inte bry sig om den här inställningen.
