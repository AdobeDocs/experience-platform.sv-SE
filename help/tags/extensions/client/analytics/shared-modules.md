---
title: Delade moduler för Adobe Analytics-tillägget
description: Lär dig mer om de delade biblioteksmodulerna i Adobe Analytics-taggtillägget i Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Delade moduler för Adobe Analytics-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

The [Adobe Analytics-tillägg](./overview.md) innehåller två olika [delade moduler](../../../extension-dev/web/shared.md) som ni kan integrera i era upplevelseapplikationer. Dessa moduler beskrivs i avsnitten nedan.

## [!DNL get-tracker]

Innan Adobe Analytics skickar några beacons måste spårningsobjektet initieras. Initieringsprocessen börjar med att läsa in [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html), följt av att skapa ett spårningsobjekt.

Du kommer åt spårningsobjektet efter att det har initierats fullständigt med hjälp av `get-tracker` delad modul enligt följande:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Verifierar att Adobe Analytics har installerats

Det är möjligt att Adobe Analytics inte har installerats eller inkluderats i samma taggbibliotek som ditt tillägg. Därför rekommenderar vi att du kontrollerar detta fall i koden och hanterar det på rätt sätt. Följande JavaScript är ett exempel på hur du kan implementera detta:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

If `getTracker` är `undefined`, finns inte Adobe Analytics-tillägget i taggbiblioteket. Du kan anpassa det loggade meddelandet så att det korrekt återspeglar vilka funktioner som kan förloras om Adobe Analytics inte är installerat.


## [!DNL augment-tracker]

När spårningsobjektet har initierats utökas nästa steg i processen. I det här steget kan tillägget förstärka spåraren med allt som behövs innan några variabler har tillämpats från Adobe Analytics-tilläggskonfigurationen eller innan några signaler har skickats.

Dessutom har tillägget möjlighet att pausa initieringsprocessen för spåraren medan tillägget utför en egen asynkron åtgärd, som att hämta data eller JavaScript från en server.

Du kan implementera `augment-tracker` i en sådan modul:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

Funktionen som skickades till `augmentTracker()` kommer att anropas så snart som den förstärkande fasen av initieringsprocessen för spåraren har nåtts.

Om ditt tillägg måste slutföra en asynkron åtgärd innan spåraren utökas kan du returnera ett löfte från din funktion enligt följande:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Genom att returnera ett löfte signalerar ditt tillägg till Adobe Analytics att det ska pausa initieringsprocessen för spåraren tills löftet är löst.

>[!WARNING]
>
>Var försiktig när du pausar initieringsprocessen för spåraren eftersom det kan fördröja att beacons skickas och därför resultera i oinsamlade data (om användaren till exempel navigerar bort från sidan innan beacon skickas).
