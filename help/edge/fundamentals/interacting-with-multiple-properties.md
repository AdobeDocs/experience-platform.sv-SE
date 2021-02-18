---
title: Interagera med flera egenskaper i Adobe Experience Platform Web SDK
description: Lär dig hur du interagerar med flera Experience Platform Web SDK-egenskaper.
keywords: flera egenskaper;konfigurera;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Interagera med flera egenskaper

I vissa fall kanske du vill interagera med två olika egenskaper på samma sida. Bland dessa finns:

* Företag som har förvärvats och arbetar med att integrera sina webbplatser tillsammans
* Datadelningsrelationer mellan flera företag
* Kunder som testar nya Adobe-lösningar och inte vill störa sin befintliga implementering

Med SDK kan du skapa en separat instans för varje egenskap genom att lägga till ett annat namn till arrayen i baskoden. I följande exempel har vi angett två namn, `mycustomname1` och `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Därför skapar skriptet två instanser av SDK. Den globala funktionen för interaktion med den första instansen heter `mycustomname1` och den globala funktionen för interaktion med den andra instansen heter `mycustomname2`.

Genom att skapa två separata instanser kan varje instans konfigureras för en annan egenskap. All kommunikation eller databeständighet som inträffar på grund av interaktion med `mycustomname1` hålls isolerad från `mycustomname2` och vice versa.

I följande exempel kan du köra kommandon med var och en av instanserna:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Var noga med att köra kommandot `configure` för varje instans innan du kör andra kommandon på samma instans.

## Begränsningar

För att undvika konflikter med cookies kan bara en instans av Adobe Experience Platform [!DNL Web SDK] på en sida ha en viss `edgeConfigId`.  På samma sätt kan bara en instans av Adobe Experience Platform [!DNL Web SDK] ha en viss `orgId`.
