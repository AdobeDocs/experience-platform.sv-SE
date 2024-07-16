---
title: edgeBasePath
description: Bassökvägen för slutpunkten som används för att interagera med Adobes tjänster.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 1%

---

# `edgeBasePath`

Egenskapen `edgeBasePath` ändrar målsökvägen när du interagerar med Adobe-tjänster. De flesta organisationer behöver inte ange eller ändra den här egenskapen.

## Edge bassökväg med tillägget Web SDK-tagg

Ange önskad text i textfältet **[!UICONTROL Edge base path]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Rulla ned till avsnittet [!UICONTROL Advanced Settings] och ange önskat värde i textfältet **[!UICONTROL Edge base path]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Edge bassökväg med Web SDK JavaScript-biblioteket

Ange textfältet `edgeBasePath` när du kör kommandot `configure`. Om du utelämnar den här egenskapen blir standardvärdet `ee`. Adobe rekommenderar att du utelämnar den här egenskapen från de flesta konfigurationer.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
