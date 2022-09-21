---
title: Installera Adobe Experience Platform Web SDK
description: Lär dig hur du installerar Experience Platform Web SDK.
keywords: web sdk-installation;installera web sdk;Internet Explorer;promise;npm-paket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Installera SDK {#installing-the-sdk}

Det finns tre sätt att använda Adobe Experience Platform Web SDK som stöds:

1. Det bästa sättet att använda Adobe Experience Platform Web SDK är via användargränssnittet för datainsamling eller användargränssnittet för Experience Platform.
1. Adobe Experience Platform Web SDK finns också i ett leveransnätverk (CDN) som du kan använda.
1. Använd NPM-biblioteket som exporterar EcmaScript 5- och EcmaScript 2015-moduler (ES6).

## Alternativ 1: Installera taggtillägget

Dokumentation om taggtillägget finns i [startdokumentation](../../tags/extensions/web/sdk/overview.md)

## Alternativ 2: Installera den fördefinierade fristående versionen

Den färdiga versionen finns på ett CDN. Du kan referera till biblioteket på CDN direkt på din sida eller hämta och lagra det på din egen infrastruktur. Den finns i minifierade och ominifierade format. Den ominiatyrversionen är användbar i felsökningssyfte.

URL-struktur: https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js OR alloy.js för den icke-minifierade versionen.

Exempel:


* Miniatyrbild: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Unminified: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)


### Lägga till koden {#adding-the-code}

Den fördefinierade fristående versionen kräver en &quot;baskod&quot; som läggs till direkt på sidan. Kopiera och klistra in följande &quot;baskod&quot; så hög som möjligt i `<head>` -tagg på HTML:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

&quot;Baskod&quot; skapar en global funktion med namnet `alloy`. Använd den här funktionen för att interagera med SDK:n. Om du vill ge den globala funktionen ett annat namn ändrar du `alloy` namn enligt följande:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
```

I det här exemplet byter den globala funktionen namn `mycustomname`, i stället för `alloy`.

>[!IMPORTANT]
>
>Undvik potentiella problem genom att använda ett namn som innehåller minst ett tecken som inte är en siffra och som inte står i konflikt med namnet på en egenskap som redan hittats på `window`.

Utöver att skapa en global funktion läser den här baskoden in ytterligare kod som finns i en extern fil \(`alloy.js`\) lagras på en server. Som standard läses den här koden in asynkront så att webbsidan kan fungera så bra som möjligt. Detta är den rekommenderade implementeringen.

### Stöd för Internet Explorer {#support-internet-explore}

Denna SDK använder löften, som är ett sätt att kommunicera slutförandet av asynkrona uppgifter. The [Lova](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementering som används av SDK stöds internt av alla målwebbläsare utom [!DNL Internet Explorer]. Så här använder du SDK på [!DNL Internet Explorer]måste du ha `window.Promise` [polyfylld](https://remysharp.com/2010/10/08/what-is-a-polyfill).

För att avgöra om du redan har `window.Promise` polyfylld:

1. Öppna webbplatsen i [!DNL Internet Explorer].
1. Öppna webbläsarens felsökningskonsol.
1. Typ `window.Promise` till konsolen och tryck sedan på Retur.

Om något annat än `undefined` visas, du har antagligen redan polyfyllt `window.Promise`. Ett annat sätt att avgöra om `window.Promise` fylls i genom att webbplatsen läses in när ovanstående installationsanvisningar är klara. Om SDK genererar ett fel som talar om något om ett löfte har du troligen inte polyfyllt `window.Promise`.

Om du har bestämt att du måste polyfyll `window.Promise`inkluderar du följande script-tagg ovanför den tidigare angivna baskoden:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Den här taggen läser in ett skript som ser till att `window.Promise` är en giltig Promise-implementering.

>[!NOTE]
>
>Om du väljer att läsa in en annan Promise-implementering måste den ha stöd för `Promise.prototype.finally`.

### Läsa in JavaScript-filen synkront {#loading-javascript-synchronously}

Se avsnittet [Lägga till koden](#adding-the-code), kommer den baskod som du har kopierat och klistrat in på webbplatsens HTML att läsa in en extern fil. Den externa filen innehåller SDK:ns kärnfunktioner. Alla kommandon som du försöker köra när den här filen läses in är köade och bearbetas sedan när filen har lästs in. Inläsning av filen asynkront är den mest prestandametoden vid installation.

Under vissa omständigheter kanske du vill läsa in filen synkront \(mer information om dessa omständigheter beskrivs senare\). Om du gör det blockeras resten av HTML-dokumentet från att tolkas och återges av webbläsaren tills den externa filen har lästs in och körts. Denna ytterligare fördröjning innan primärt innehåll visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på omständigheterna.

Om du vill läsa in filen synkront i stället för asynkront tar du bort `async` attribut från andra `script` tagg enligt nedan:

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

Adobe Experience Platform Web SDK finns också som NPM-paket. [NPM](https://www.npmjs.com) är pakethanteraren för JavaScript. Genom att installera NPM-paketet får du kontroll över byggprocessen för Adobe Experience Platform Web SDK JavaScript. NPM-paketet visar EcmaScript version 5-moduler eller EcmaScript version 2015-moduler (ES6) som ska köras i webbläsaren.

```bash
npm install @adobe/alloy
```

NPM-paketet för Adobe Experience Platform Web SDK visar en `createInstance` funktion. Den här funktionen används för att skapa en instans. Namnalternativet som skickas till funktionen styr det prefix som används vid loggning. Nedan finns exempel på hur du använder paketet.

### Använda paketet som en ECMAScript 2015-modul (ES6)

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM-paketet bygger på CommonJS-moduler. När du använder ett paket måste du därför se till att paketet har stöd för CommonJS-moduler. Vissa paket, som [Samlad](https://rollupjs.org), kräver [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) som har stöd för CommonJS.

### Använda paketet som en ECMAScript 5-modul

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### Stöd för Internet Explorer

Adobe Experience Platform SDK använder löften, som är ett sätt att kommunicera slutförandet av asynkrona uppgifter. The [Lova](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) implementering som används av SDK stöds internt av alla målwebbläsare utom [!DNL Internet Explorer]. Så här använder du SDK på [!DNL Internet Explorer]måste du ha `window.Promise` [polyfylld](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Ett bibliotek som man kan använda för att polyfill-löftet är en utfästelse-polyfill. Se [dokumentation för promise-polyfill](https://www.npmjs.com/package/promise-polyfill) för mer information om hur du installerar med NPM.

>[!NOTE]
>
>Om du väljer att läsa in en annan Promise-implementering måste den ha stöd för `Promise.prototype.finally`.
