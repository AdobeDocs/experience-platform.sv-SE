---
title: idMigrationEnabled
description: Gör att Web SDK kan läsa AMCV-cookies.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# `idMigrationEnabled`

The `idMigrationEnabled` kan Web SDK läsa AMCV-cookies som angetts av tidigare Adobe Experience Cloud-implementeringar. Om din organisation uppgraderar din implementering till Web SDK, ger den här inställningen en smidigare övergång till den aktuella Adobe Experience Cloud ID-tjänsten. Den här inställningen är värdefull så att du inte ser en kraftig ökning av antalet unika besökare när du uppgraderar till Web SDK.

Om din organisation kör en ny Web SDK-implementering har aktiveringen av den här inställningen ingen effekt på datainsamling eller besöksidentifiering. Det finns inga nackdelar med att låta det vara aktiverat för alla implementeringar.

## Aktivera ID-migrering med taggtillägget Web SDK

Välj **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Leta reda på [!UICONTROL Identity] markerar du kryssrutan **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Aktivera ID-migrering med JavaScript-biblioteket för Web SDK

Ange `idMigrationEnabled` boolesk när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange den här egenskapen om du vill inaktivera möjligheten att läsa AMCV-cookies som angetts av Visitor API. De flesta organisationer behöver inte ange den här egenskapen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
