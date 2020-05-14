---
title: Installera Adobe Experience Platform Web SDK
seo-title: Adobe Experience Platform Web SDK installerar SDK
description: Lär dig hur du installerar Experience Platform Web SDK
seo-description: Lär dig hur du installerar Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 5998473c665cb80ffddc092847533f51d81cf581
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# Installera SDK

AEP web SDK finns på ett CDN som du kan använda. Du kan referera till den här filen eller ladda ned den och lagra den i din egen infrastruktur. Den finns i minifierad och icke-minifierad version. Den version som inte är miniatyrversion är användbar i felsökningssyfte.

[https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js)[https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js](https://cdn1.adoberesources.net/alloy/1.0.0/alloy.js)

## Lägga till koden

Det första steget i implementeringen av Adobe Experience Platform Web SDK är att kopiera och klistra in följande &quot;baskod&quot; så hög som möjligt i HTML-taggen: `<head>`

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

Baskoden skapar en global funktion med namnet `alloy`. Använd den här funktionen för att interagera med SDK:n. Om du vill ge den globala funktionen ett annat namn kan du ändra `alloy` namnet enligt följande:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js" async></script>
```

I det här exemplet byter den globala funktionen namn `mycustomname`i stället för `alloy`.

>[!IMPORTANT]
>Undvik potentiella problem genom att använda ett namn som innehåller minst ett tecken som inte är en siffra och som inte står i konflikt med namnet på en egenskap som redan hittats på `window`.

Utöver att skapa en global funktion läser den här baskoden även in ytterligare kod som finns i en extern fil \(`alloy.js`\) som finns på en server. Som standard läses den här koden in asynkront så att webbsidan kan fungera så bra som möjligt. Detta är den rekommenderade implementeringen.

## Stöd för Internet Explorer

Denna SDK använder löften, som är ett sätt att förmedla slutförandet av asynkrona uppgifter. Den implementering av [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) som används av SDK stöds internt av alla målwebbläsare utom Internet Explorer. Om du vill använda SDK i Internet Explorer måste du ha `window.Promise` fyllt i [i](https://remysharp.com/2010/10/08/what-is-a-polyfill)texten.

Så här kontrollerar du om du redan har `window.Promise` polyfyllda:

1. Öppna webbplatsen i Internet Explorer.
1. Öppna webbläsarens felsökningskonsol.
1. Skriv `window.Promise` in i konsolen och tryck sedan på Retur.

Om något annat än `undefined` visas har du troligen redan polyifyllt `window.Promise`. Ett annat sätt att avgöra om `window.Promise` är polyfylld är att läsa in webbplatsen efter att ha slutfört installationsinstruktionerna ovan. Om SDK genererar ett fel som talar om något om ett löfte har du troligen inte polyfyllt `window.Promise`.

Om du har fastställt att du måste polyfylla `window.Promise`i, inkluderar du följande script-tagg ovanför den tidigare angivna baskoden:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Detta läser in ett skript som ser till att `window.Promise` det är en giltig Promise-implementering.

## Läsa in JavaScript-filen synkront

Baskoden som du har kopierat och klistrat in i webbplatsens HTML-kod läser som förklarats ovan in en extern fil med ytterligare kod. Den här extra koden innehåller SDK:s kärnfunktioner. Alla kommandon som du försöker köra medan den här filen läses in är köade och bearbetas sedan när filen har lästs in. Det här är den mest prestandametoden vid installation.

Under vissa omständigheter kanske du vill läsa in filen synkront \(mer information om dessa omständigheter beskrivs senare\). Om du gör det blockeras resten av HTML-dokumentet från att tolkas och återges av webbläsaren tills den externa filen har lästs in och körts. Denna ytterligare fördröjning innan primärt innehåll visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på omständigheterna.

Om du vill läsa in filen synkront i stället för asynkront tar du bort attributet från den andra `async` `script` -taggen enligt nedan:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/1.0.0/alloy.min.js"></script>
```
