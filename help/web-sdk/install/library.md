---
title: Installera Web SDK med JavaScript-biblioteket
description: Referera till Web SDK-biblioteket med en fristående CDN-fil.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Installera Web SDK med JavaScript-biblioteket

Ett alternativ till att installera Web SDK utan [att använda taggtillägget](extension.md) är att referera till JavaScript-biblioteket som finns på ett CDN. Du kan referera till biblioteket direkt eller hämta det och lagra det i din egen infrastruktur. Det finns i miniformat och fullt format.

Web SDK-biblioteket är tillgängligt med följande URL-struktur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Fullständig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Se [versionsinformationen](../release-notes.md) för den senaste versionen som ska inkluderas i URL:en. URL:en för den fullständiga versionen av version 2.19.1 är till exempel `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Lägga till koden

Lägg till följande kodblock så högt som möjligt i taggen `<head>` på HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Med den här koden skapas ett `alloy`-objekt asynkront som gör att du kan anropa ett Web SDK-kommando. Om du vill läsa in Web SDK synkront kan du ta bort attributet `async` på den sista raden i kodblocket. Om attributet `async` tas bort blockeras resten av HTML-dokumentet från att tolkas och återges av webbläsaren tills biblioteket har lästs in och körts. Denna ytterligare fördröjning innan det primära innehållet visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på organisationens behov.
