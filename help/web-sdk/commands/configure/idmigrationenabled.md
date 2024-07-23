---
title: idMigrationEnabled
description: Gör att Web SDK kan läsa AMCV-cookies.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# `idMigrationEnabled`

Egenskapen `idMigrationEnabled` gör att Web SDK kan läsa AMCV-cookies som angetts av tidigare Adobe Experience Cloud-implementeringar. Om din organisation uppgraderar din implementering till Web SDK, ger den här inställningen en smidigare övergång till den aktuella Adobe Experience Cloud ID-tjänsten. Den här inställningen är värdefull så att du inte ser en kraftig ökning av antalet unika besökare när du uppgraderar till Web SDK.

Om din organisation kör en ny Web SDK-implementering har aktiveringen av den här inställningen ingen effekt på datainsamling eller besöksidentifiering. Det finns inga nackdelar med att låta det vara aktiverat för alla implementeringar.

## Aktivera ID-migrering med taggtillägget Web SDK

Markera kryssrutan **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Leta reda på avsnittet [!UICONTROL Identity] och markera kryssrutan **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Aktivera ID-migrering med Web SDK JavaScript-biblioteket

Ange det booleska värdet `idMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange den här egenskapen om du vill inaktivera möjligheten att läsa AMCV-cookies som angetts av Visitor API. De flesta organisationer behöver inte ange den här egenskapen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
