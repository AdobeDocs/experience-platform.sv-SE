---
title: Använda flera Web SDK-instanser
description: Lär dig hur du interagerar med olika egenskaper i Experience Platform Web SDK.
keywords: flera egenskaper
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Använda flera Web SDK-instanser

I vissa fall kanske du vill interagera med två olika egenskaper på samma sida. Möjliga scenarier:

* Företag som har förvärvats och arbetar med att integrera sina webbplatser tillsammans
* Datadelningsrelationer mellan flera företag
* Kunder som testar nya Adobe-lösningar och inte vill störa sin befintliga implementering

Med SDK kan du skapa en separat instans för varje egenskap genom att lägga till ett annat namn till arrayen i [baskoden](../js/install/base-code.md). Följande exempel innehåller två namn, `titanium` och `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Därför skapar skriptet två globala funktioner (`titanium` och `copper` i ovanstående exempel) som blir två SDK-instanser när biblioteket initieras. Varje instans behåller sin egen konfiguration och status. Alla kommandon som använder `titanium` hålls isolerade från `copper`.

>[!TIP]
>
>Om du använder baskoden med taggar måste alla instansnamn som du anger matcha alla [SDK-instansnamn](/help/tags/extensions/client/web-sdk/configure/general.md) när du konfigurerar taggtillägget.

Om du följer namnmönsterexemplet på `titanium` och `copper` som Web SDK-instanser kan du köra kommandon oberoende av varandra:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Var noga med att köra [`configure`](../js/commands/configure/overview.md)-kommandot för varje instans innan du kör andra kommandon på samma instans.

>[!IMPORTANT]
>
>För att undvika konflikter med cookies måste varje Web SDK-instans ha sin egen unika `datastreamId` och sin egen unika `orgId`.
