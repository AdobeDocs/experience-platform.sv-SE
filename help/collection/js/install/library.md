---
title: Installera SDK JavaScript-biblioteket
description: Referera till Web SDK-biblioteket med en fristående CDN-fil.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Installera SDK JavaScript-biblioteket

Om du väljer att inte använda [SDK-taggtillägget för webben](/help/tags/extensions/client/web-sdk/overview.md) kan du installera Web SDK genom att referera till det fristående JavaScript-biblioteket som finns på Adobe CDN. Du kan referera till biblioteket direkt eller hämta det och lagra det i din egen infrastruktur. Det finns i miniformat och fullt format.

Webbbiblioteket SDK är tillgängligt med följande URL-struktur:

* **Minified**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Fullständig**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

Se [Versionsinformationen för Web SDK](../release-notes.md) för den senaste versionen som ska ingå i URL:en. URL:en för den fullständiga versionen av version 2.19.1 är till exempel `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Lägga till baskod och biblioteksinläsare

Koden som ska läggas till består av två avsnitt:

* **Baskod**: Tillåter startspärr genom kökommandon när Web SDK läses in asynkront. Mer information finns i [Baskod](base-code.md). Adobe rekommenderar att du använder baskoden när du läser in biblioteket asynkront för att undvika konkurrensförhållanden när du anropar Web SDK-kommandon under sidinläsning.
* **Library loader**: Läser in hela JavaScript-biblioteket.

Lägg till följande kodblock så högt som möjligt i taggen `<head>`, före eventuella skript som kan anropa Web SDK:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Om du vill läsa in Web SDK synkront kan du ta bort attributet `async` när du läser in biblioteket. Om attributet `async` tas bort blockeras HTML-tolkning medan webbläsaren hämtar och kör biblioteket. Denna ytterligare fördröjning innan det primära innehållet visas för användarna rekommenderas vanligtvis inte, men den kan vara bra beroende på organisationens behov.
