---
title: edgeBasePath
description: Bassökvägen för slutpunkten som används för att interagera med Adobes tjänster.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 1fa7b48f99948a5252635dc1a8c5142fea5df57b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# `edgeBasePath`

Egenskapen `edgeBasePath` ändrar målsökvägen när du interagerar med Adobe-tjänster. Adobe kan begära att du ändrar den här variabeln om du deltar i alfa- eller betaprogram för datainsamling. De flesta organisationer behöver inte ange eller ändra den här egenskapen.

Ange textfältet `edgeBasePath` när du kör kommandot `configure`. Om du utelämnar den här egenskapen blir standardvärdet `ee`. Adobe rekommenderar att du utelämnar den här egenskapen från de flesta konfigurationer.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```

## Edge bassökväg med taggtillägget Web SDK

SDK-taggtilläggets motsvarighet för det här fältet finns under [Avancerade konfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/advanced-settings.md) när du konfigurerar taggtillägget.
