---
title: Övervaka kopplingar för Adobe Experience Platform Web SDK
description: Lär dig hur du använder övervakningsböckerna från Adobe Experience Platform Web SDK för att felsöka implementeringen och hämta Web SDK-loggar.
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 1%

---

# Övervaka hookar för Web SDK

Adobe Experience Platform Web SDK innehåller funktioner för övervakning av kopplingar som du kan använda för att övervaka olika systemhändelser. De här verktygen är användbara när du vill utveckla egna felsökningsverktyg och hämta webb-SDK-loggar.

Web SDK utlöser övervakningsfunktionerna oavsett om du har aktiverat [felsökning](commands/configure/debugenabled.md) eller inte.

## `onInstanceCreated` {#onInstanceCreated}

Den här återanropsfunktionen aktiveras när du har skapat en ny Web SDK-instans. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.instance` | Funktion | Den instansfunktion som används för att anropa Web SDK-kommandon. |

## `onInstanceConfigured` {#onInstanceConfigured}

Den här återanropsfunktionen aktiveras av Web SDK när kommandot [`configure`](commands/configure/overview.md) har lösts. I exemplet nedan finns mer information om funktionsparametrarna.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.config` | Objekt | Ett objekt som innehåller den konfiguration du använde för din Web SDK-instans. Detta är alternativen som skickas till kommandot [`configure`](commands/configure/overview.md) med alla standardvärden tillagda. |

## `onBeforeCommand` {#onBeforeCommand}

Den här återanropsfunktionen aktiveras av Web SDK innan något annat kommando körs. Du kan använda den här funktionen för att hämta konfigurationsalternativen för ett specifikt kommando. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.commandName` | Sträng | Namnet på det Web SDK-kommando före vilket den här funktionen körs. |
| `data.options` | Objekt | Ett objekt som innehåller de alternativ som skickas till Web SDK-kommandot. |

## `onCommandResolved` {#onCommandResolved}

Den här återanropsfunktionen aktiveras när kommandotolken löses. Du kan använda den här funktionen för att se kommandoalternativen och resultatet. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.commandName` | Sträng | Namnet på det körda Web SDK-kommandot. |
| `data.options` | Objekt | Ett objekt som innehåller de alternativ som skickas till Web SDK-kommandot. |
| `data.result` | Objekt | Ett objekt som innehåller resultatet av kommandot Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Den här återanropsfunktionen aktiveras innan ett kommandolöfte avvisas och den innehåller information om varför kommandot avvisades. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.commandName` | Sträng | Namnet på det körda Web SDK-kommandot. |
| `data.options` | Objekt | Ett objekt som innehåller de alternativ som skickas till Web SDK-kommandot. |
| `data.error` | Objekt | Ett objekt som innehåller felmeddelandet som returnerades från webbläsarens nätverksanrop (`fetch` i de flesta fall), tillsammans med orsaken till varför kommandot avvisades. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Den här återanropsfunktionen aktiveras innan en nätverksbegäran körs. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.requestId` | Sträng | `requestId` som genererats av Web SDK för att aktivera felsökning. |
| `data.url` | Sträng | Begärd URL. |
| `data.payload` | Objekt | Nyttolastobjektet för nätverksbegäran som konverteras till JSON-format och skickas i brödtexten för begäran via en `POST`-metod. |

## `onNetworkResponse` {#onNetworkResponse}

Den här återanropsfunktionen aktiveras när webbläsaren får ett svar. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.requestId` | Sträng | `requestId` som genererats av Web SDK för att aktivera felsökning. |
| `data.url` | Sträng | Begärd URL. |
| `data.payload` | Objekt | Nyttolastobjektet som ska konverteras till JSON-format och skickas i förfrågningens brödtext via en `POST`-metod. |
| `data.body` | Sträng | Svarstexten i strängformat. |
| `data.parsedBody` | Objekt | Ett objekt som innehåller den tolkade svarstexten. Om ett fel inträffar när svarstexten analyseras är den här parametern odefinierad. |
| `data.status` | Sträng | Svarskoden i heltalsformat. |
| `data.retriesAttempted` | Heltal | Antal försök att skicka begäran. Noll innebär att begäran lyckades vid första försöket. |

## `onNetworkError` {#onNetworkError}

Den här återanropsfunktionen aktiveras när nätverksbegäran misslyckas. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.requestId` | Sträng | `requestId` som genererats av Web SDK för att aktivera felsökning. |
| `data.url` | Sträng | Begärd URL. |
| `data.payload` | Objekt | Nyttolastobjektet som ska konverteras till JSON-format och skickas i förfrågningens brödtext via en `POST`-metod. |
| `data.error` | Objekt | Ett objekt som innehåller felmeddelandet som returnerades från webbläsarens nätverksanrop (`fetch` i de flesta fall), tillsammans med orsaken till varför kommandot avvisades. |

## `onBeforeLog` {#onBeforeLog}

Den här återanropsfunktionen aktiveras innan Web SDK loggar något till konsolen. I exemplet nedan finns mer information om funktionsparametrarna.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.componentName` | Sträng | Namnet på komponenten som genererade loggmeddelandet. |
| `data.level` | Sträng | Loggningsnivån. Nivåer som stöds: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Strängarray | Loggmeddelandets argument. |


## `onContentRendering` {#onContentRendering}

Den här återanropsfunktionen aktiveras av komponenten `personalization` i olika återgivningsfaser. Nyttolasten kan variera beroende på parametern `status`. I exemplet nedan finns mer information om funktionsparametrarna.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.componentName` | Sträng | Namnet på komponenten som genererade loggmeddelandet. |
| `data.payload` | Objekt | Nyttolastobjektet som ska konverteras till JSON-format och skickas i förfrågningens brödtext via en `POST`-metod. |
| `data.status` | Sträng | Komponenten `personalization` meddelar Web SDK om återgivningsstatus.  Värden som stöds: <ul><li>`rendering-started`: Anger att Web SDK ska återge förslag. Innan Web SDK börjar återge ett beslutsområde eller en vy kan du i objektet `data` se de förslag som ska återges av komponenten `personalization` och scopenamnet.</li><li>`no-offers`: Anger att ingen nyttolast har tagits emot för de begärda parametrarna.</li> <li>`rendering-failed`: Anger att Web SDK inte kunde återge ett förslag.</li><li>`rendering-succeeded`: Anger att återgivningen har slutförts för ett beslutsområde.</li> <li>`rendering-redirect`: Anger att Web SDK ska återge ett omdirigeringsförslag.</li></ul> |

## `onContentHiding` {#onContentHiding}

Den här återanropsfunktionen aktiveras när ett fördolt format används eller tas bort.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parameter | Typ | Beskrivning |
|---------|----------|----------|
| `data.instanceName` | Sträng | Namnet på den globala variabeln där Web SDK-instansen lagras. |
| `data.componentName` | Sträng | Namnet på komponenten som genererade loggmeddelandet. |
| `data.status` | Sträng | Komponenten `personalization` meddelar Web SDK om återgivningsstatus. Värden som stöds: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Ange övervakningskopplingar när NPM-paketet används {#specify-monitoring-npm}

Om du använder Web SDK via [NPM-paketet](install/npm.md) kan du ange övervakningskopplingar i funktionen `createInstance` enligt nedan.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Exempel {#example}

Web SDK söker efter en objektmatris i en global variabel som heter `__alloyMonitors`.

Om du vill spela in alla Web SDK-händelser måste du definiera övervakningsböckerna innan Web SDK-koden läses in på sidan. Varje övervakningsmetod hämtar en Web SDK-händelse.

Du kan definiera övervakningskopplingar *när* Web SDK-kod har lästs in på sidan, men alla kopplingar som har utlösts före sidinläsning *hämtas* inte.

När du definierar ett övervakningsobjekt behöver du bara definiera de metoder som du vill definiera en speciell logik för.
Om du till exempel bara bryr dig om `onContentRendering` kan du bara definiera den metoden. Du behöver inte använda alla övervakningskopplingar samtidigt.

Du kan definiera flera övervakningsanslutna kromobjekt. Alla objekt med den angivna metoden anropas när motsvarande händelse aktiveras.

>[!TIP]
>
>Nedan visas en exempelsida med alla övervakningskopplingar implementerade.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
