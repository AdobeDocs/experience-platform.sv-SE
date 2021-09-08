---
title: Installera Adobe Experience Platform Web SDK
description: Lär dig hur du installerar Experience Platform Web SDK.
keywords: web sdk-installation;installera web sdk;Internet Explorer;promise;npm-paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f5d3c5911357d4b76e4d38564bf637e2549469d6
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Installera SDK {#installing-the-sdk}

Det finns tre sätt att använda Adobe Experience Platform Web SDK som stöds:

1. Det bästa sättet att använda Adobe Experience Platform Web SDK är via användargränssnittet för datainsamling.
1. Adobe Experience Platform Web SDK finns också i ett leveransnätverk (CDN) som du kan använda.
1. Använd NPM-biblioteket som exporterar EcmaScript 5- och EcmaScript 2015-moduler (ES6).

## Alternativ 1: Installera taggtillägget

Dokumentation om taggtillägget finns i [startdokumentationen](../../tags/extensions/web/sdk/overview.md)

## Alternativ 2: Installera den fördefinierade fristående versionen

Den färdiga versionen finns på ett CDN. Du kan referera till biblioteket på CDN direkt på din sida eller hämta och lagra det på din egen infrastruktur. Den finns i minifierade och ominifierade format. Den ominiatyrversionen är användbar i felsökningssyfte.

URL-struktur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js for the non-minified version.

Exempel:


* Miniatyrbild: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Unminified: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### Lägga till koden {#adding-the-code}

Den fördefinierade fristående versionen kräver en &quot;baskod&quot; som läggs till direkt på sidan. Kopiera och klistra in följande&quot;baskod&quot; så hög som möjligt i taggen `<head>` i din HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

Med &quot;baskod&quot; skapas en global funktion med namnet `alloy`. Använd den här funktionen för att interagera med SDK:n. Om du vill ge den globala funktionen ett annat namn ändrar du `alloy`-namnet så här:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

I det här exemplet byter den globala funktionen namn till `mycustomname` i stället för `alloy`.

>[!IMPORTANT]
>
>Undvik potentiella problem genom att använda ett namn som innehåller minst ett tecken som inte är en siffra och som inte står i konflikt med namnet på en egenskap som redan finns i `window`.

Utöver att skapa en global funktion läser den här baskoden även in ytterligare kod som finns i den externa filen \(`alloy.js`\) som finns på en server. Som standard läses den här koden in asynkront så att webbsidan kan fungera så bra som möjligt. Detta är den rekommenderade implementeringen.

### Stöd för Internet Explorer {#support-internet-explore}

Denna SDK använder löften, som är ett sätt att kommunicera slutförandet av asynkrona uppgifter. Den [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-implementering som används av SDK stöds av alla målwebbläsare förutom [!DNL Internet Explorer]. Om du vill använda SDK på [!DNL Internet Explorer] måste du ha `window.Promise` [polyfyllt](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Så här kontrollerar du om du redan har `window.Promise` polyierat:

1. Öppna webbplatsen i [!DNL Internet Explorer].
1. Öppna webbläsarens felsökningskonsol.
1. Skriv `window.Promise` i konsolen och tryck sedan på Retur.

Om något annat än `undefined` visas har du troligen redan polyifierat `window.Promise`. Ett annat sätt att avgöra om `window.Promise` är polyfyllt är att läsa in webbplatsen efter att ha slutfört installationsinstruktionerna ovan. Om SDK genererar ett fel som anger något om ett löfte har du troligen inte polyfyllt `window.Promise`.

Om du har fastställt att du måste polyfill `window.Promise`, inkluderar du följande script-tagg ovanför den tidigare angivna baskoden:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Den här taggen läser in ett skript som ser till att `window.Promise` är en giltig Promise-implementering.

>[!NOTE]
>
>Om du väljer att läsa in en annan Promise-implementering måste den ha stöd för `Promise.prototype.finally`.

### Läsa in JavaScript-filen synkront {#loading-javascript-synchronously}

Så som förklaras i avsnittet [Om du lägger till koden](#adding-the-code), läses den baskod som du har kopierat och klistrat in i webbplatsens HTML in som en extern fil. Den externa filen innehåller SDK:ns kärnfunktioner. Alla kommandon som du försöker köra när den här filen läses in är köade och bearbetas sedan när filen har lästs in. Inläsning av filen asynkront är den mest prestandametoden vid installation.

Under vissa omständigheter kanske du vill läsa in filen synkront \(mer information om dessa omständigheter beskrivs senare\). Om du gör det blockeras resten av HTML-dokumentet från att tolkas och återges av webbläsaren tills den externa filen har lästs in och körts. Denna ytterligare fördröjning innan primärt innehåll visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på omständigheterna.

Om du vill läsa in filen synkront i stället för asynkront tar du bort attributet `async` från den andra `script`-taggen enligt nedan:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js"></script>
```

## Alternativ 3: Använda NPM-paketet

Adobe Experience Platform Web SDK finns också som NPM-paket. [](https://www.npmjs.com) NPM är pakethanteraren för JavaScript. Genom att installera NPM-paketet får du kontroll över byggprocessen för Adobe Experience Platform Web SDK JavaScript. NPM-paketet visar EcmaScript version 5-moduler eller EcmaScript version 2015-moduler (ES6) som ska köras i webbläsaren.

```bash
npm install @adobe/alloy
```

NPM-paketet för Adobe Experience Platform Web SDK visar en `createInstance`-funktion. Den här funktionen används för att skapa en instans. Namnalternativet som skickas till funktionen styr det prefix som används vid loggning. Nedan finns exempel på hur du använder paketet.

### Använda paketet som en ECMAScript 2015-modul (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM-paketet bygger på CommonJS-moduler. När du använder ett paket måste du därför se till att paketet har stöd för CommonJS-moduler. Vissa paketerare, till exempel [Rollup](https://rollupjs.org), kräver ett [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) som har stöd för CommonJS.

### Använda paketet som en ECMAScript 5-modul

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Stöd för Internet Explorer

Adobe Experience Platform SDK använder löften, som är ett sätt att kommunicera slutförandet av asynkrona uppgifter. Den [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)-implementering som används av SDK stöds av alla målwebbläsare förutom [!DNL Internet Explorer]. Om du vill använda SDK på [!DNL Internet Explorer] måste du ha `window.Promise` [polyfyllt](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Ett bibliotek som man kan använda för att polyfill-löftet är en utfästelse-polyfill. Mer information om hur du installerar med NPM finns i [dokumentationen för promise-polyfill](https://www.npmjs.com/package/promise-polyfill).

>[!NOTE]
>
>Om du väljer att läsa in en annan Promise-implementering måste den ha stöd för `Promise.prototype.finally`.
