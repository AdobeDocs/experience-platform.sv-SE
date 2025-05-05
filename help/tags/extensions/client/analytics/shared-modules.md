---
title: Delade moduler för Adobe Analytics-tillägget
description: Lär dig mer om de delade biblioteksmodulerna i Adobe Analytics-taggtillägget i Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Delade moduler för Adobe Analytics-tillägget

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

[Adobe Analytics-tillägget](./overview.md) innehåller två olika [delade moduler](../../../extension-dev/web/shared.md) som du kan integrera i ditt upplevelseprogram. Dessa moduler beskrivs i avsnitten nedan.

## [!DNL get-tracker]

Innan Adobe Analytics skickar några beacons måste spårningsobjektet initieras. Initieringsprocessen börjar med att läsa in [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=sv-SE), följt av att skapa ett spårarobjekt.

Du kan komma åt spårningsobjektet efter att det har initierats fullständigt med den delade modulen `get-tracker` enligt följande:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Verifierar att Adobe Analytics har installerats

Det är möjligt att Adobe Analytics inte har installerats eller inkluderats i samma taggbibliotek som tillägget. Därför rekommenderar vi att du söker efter det här fallet i koden och hanterar det på rätt sätt. Följande JavaScript är ett exempel på hur du kan implementera detta:

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

Om `getTracker` är `undefined` finns inte Adobe Analytics-tillägget i taggbiblioteket. Du kan anpassa det loggade meddelandet så att det korrekt återspeglar vilka funktioner som kan förloras om Adobe Analytics inte är installerat.


## [!DNL augment-tracker]

När spårningsobjektet har initierats utökas nästa steg i processen. I det här steget kan tillägget förstärka spåraren med allt som behövs innan några variabler har tillämpats från Adobe Analytics-tilläggskonfigurationen eller innan några signaler har skickats.

Dessutom har tillägget möjlighet att pausa initieringsprocessen för spåraren medan tillägget utför en egen asynkron åtgärd, som att hämta data eller JavaScript från en server.

Du kan implementera modulen `augment-tracker` på följande sätt:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

Funktionen som skickas till `augmentTracker()` anropas så snart utökningen av initieringsprocessen för spåraren har nåtts.

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
