---
title: Baskod
description: Köa kommandon (bootstrap) medan datainsamlingsbiblioteket läses in asynkront.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Baskod

Baskoden möjliggör startsvällning genom att kökommandon köas medan Adobe Experience Platform Web SDK läses in asynkront. När baskoden har körts kan du omedelbart anropa ett kommando som [`configure`](../commands/configure/overview.md) eller [`sendEvent`](../commands/sendevent/overview.md) utan att behöva oroa dig för spårningsförhållanden eller tidpunkten för biblioteket när det har lästs in. När Web SDK har lästs in klart körs köade kommandon i en första-in-och-ut-ordning (samma ordning som de placerades i kö).

Kommandon returnerar löften, även om de står i kö. Om ett kommando står i kö tolkas eller avvisas Promise när kommandot körs när inläsningen av Web SDK är klar. Om Web SDK aldrig slutar läsas in (biblioteket kan till exempel inte läsas in) väntar löften som står i kö.

## Lägg till baskoden

Placera baskoden så hög som möjligt i taggen `<head>`, före eventuella skript som kan anropa Web SDK.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

När du har lagt till baskoden läser du in Web SDK med den valda metoden ([JavaScript-biblioteksinläsaren](library.md) eller [tagginbäddningskod](/help/tags/extensions/client/web-sdk/getting-started.md)). För taggbaserade implementeringar stöds baskoden i SDK-taggtillägget Web 2.34.0 och senare.

Den här baskoden är **inte** nödvändig i följande scenarier:

* Om du läser in JavaScript bibliotek synkront. Synkron tolkning av inläsningsblock när biblioteket hämtas och körs.
* Om du använder taggtillägget görs alla anrop till Web SDK i taggregler eller -åtgärder. Du behöver bara inkludera baskoden om implementeringen refererar till Web SDK utanför taggbiblioteket. De flesta taggitimeringar anropar vanligtvis inte Web SDK utanför taggbiblioteket, så de flesta taggitimeringar kräver inte baskoden.

## Exempel

Se kommentarerna i det här kodexemplet för att förstå hur kommandona köas och löses. Det här exemplet gäller både JavaScript-biblioteket och taggtillägget:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## Byt namn på SDK-instans

Du kan byta namn på den globala funktionen som du anropar genom att ändra den sista raden i baskoden. Ändra:

```js
(window,["alloy"]);
```

Till:

```js
(window,["ingot"]);
```

Med den här ändringen kan du anropa kommandon med `ingot` i stället för `alloy`:

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Flera SDK-instanser

Du kan också använda baskoden för att konfigurera mer än en SDK-instans på en sida. Mer information finns i [Använd flera Web SDK-instanser](../../use-cases/multiple-instances.md).
