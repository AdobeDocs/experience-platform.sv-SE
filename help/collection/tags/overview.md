---
title: Satellitobjektreferens
description: Lär dig mer om objektet _satellit på klientsidan och de olika funktioner du kan utföra med det i taggar.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `_satellite` objektreferens

Objektet `_satellite` visar flera startpunkter som stöds och som hjälper dig att interagera med det taggbibliotek som publicerats på din plats. Alla taggdistributioner visar `_satellite` om loader-taggen implementeras korrekt. Det finns flera primära användningsområden för det här objektet:

* Användning i taggbiblioteket i anpassade kodblock, vilket ger dig full tillgång till själva taggbiblioteket.
* Felsöka din driftsatta implementering i valfri miljö (utveckling, staging eller produktion)
* Direkt implementering på din webbplats, vilket ger dig full kontroll över när händelser eller taggregler utlöses. För nya implementeringar rekommenderar Adobe att du använder en mer flexibel strategi som [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Om du anropar `_satellite` från din webbplatskod (till exempel `_satellite.track()`) **skyddar du alla samtal** så att din webbplats inte är nära kopplad till taggbiblioteket.
>
>Om du använder `_satellite` i en taggegenskap eller lokalt i webbläsarkonsolen krävs ingen övervakning.

## Exempel på vanliga användningsområden

```js
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
