---
title: Installera Web SDK med JavaScript-biblioteket
description: Referera till Web SDK-biblioteket med en fristående CDN-fil.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Installera Web SDK med JavaScript-biblioteket

Ett alternativ för att installera Web SDK är att referera till JavaScript-biblioteket som finns på ett CDN. Du kan referera till biblioteket direkt eller hämta det och lagra det i din egen infrastruktur. Det finns i miniformat och fullt format.

Web SDK-biblioteket är tillgängligt med följande URL-struktur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Fullständig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Se [versionsinformation](../release-notes.md) för den senaste versionen som ska inkluderas i webbadressen. URL:en för den fullständiga versionen av version 2.19.1 är till exempel `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Lägga till koden

Lägg till följande kodblock så högt som möjligt i `<head>` -tagg på HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Med den här koden skapas en `alloy` som gör att du kan anropa ett Web SDK-kommando. Om du vill läsa in Web SDK synkront kan du ta bort `async` i den sista raden i kodblocket. Tar bort `async` blockerar resten av HTML-dokumentet från att tolkas och återges av webbläsaren tills biblioteket har lästs in och körts. Denna ytterligare fördröjning innan det primära innehållet visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på organisationens behov.
