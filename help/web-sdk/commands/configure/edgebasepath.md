---
title: edgeBasePath
description: Bassökvägen för slutpunkten som används för att interagera med Adobes tjänster.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 1%

---

# `edgeBasePath`

The `edgeBasePath` ändrar målsökvägen när du interagerar med Adobe-tjänster. De flesta organisationer behöver inte ange eller ändra den här egenskapen.

## Edge base path using the Web SDK tag extension

Ange önskad text i dialogrutan **[!UICONTROL Edge base path]** textfält när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Advanced Settings] anger du ett värde i dialogrutan **[!UICONTROL Edge base path]** textfält.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Edge base path using the Web SDK JavaScript library

Ange `edgeBasePath` textfält när `configure` -kommando. Om du utelämnar den här egenskapen blir standardvärdet `ee`. Adobe rekommenderar att du utelämnar den här egenskapen från de flesta konfigurationer.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
