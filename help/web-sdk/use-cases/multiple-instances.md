---
title: Använda flera Web SDK-instanser
description: Lär dig hur du interagerar med flera Experience Platform Web SDK-egenskaper.
keywords: flera egenskaper
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Använda flera Web SDK-instanser

I vissa fall kanske du vill interagera med två olika egenskaper på samma sida. Exempel:

* Företag som har förvärvats och arbetar med att integrera sina webbplatser tillsammans
* Datadelningsrelationer mellan flera företag
* Kunder som testar nya Adobe-lösningar och inte vill störa sin befintliga implementering

Med SDK kan du skapa en separat instans för varje egenskap genom att lägga till ett annat namn till arrayen i baskoden. Följande exempel innehåller två namn, `titanium` och `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Därför skapar skriptet två instanser av SDK. Den globala funktionen för interaktion med den första instansen heter `titanium` och den globala funktionen för interaktion med den andra instansen heter `copper`.

Genom att skapa två separata instanser kan varje instans konfigureras för en annan egenskap. All kommunikation eller databeständighet som inträffar på grund av interaktion med `titanium` hålls isolerad från `copper`.

I följande exempel kan du köra kommandon med varje instans:

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

Var noga med att köra `configure`-kommandot för varje instans innan du kör andra kommandon på samma instans.

>[!IMPORTANT]
>
>För att undvika konflikter med cookies måste varje Web SDK-instans ha sin egen unika `datastreamId` och sin egen unika `orgId`.
