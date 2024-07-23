---
title: targetMigrationEnabled
description: Tillåt att Web SDK läser och skriver Adobe Target-cookies.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# `targetMigrationEnabled`

Egenskapen `targetMigrationEnabled` är en boolesk egenskap som gör att Web SDK kan läsa och skriva de mbox- och mboxEdgeCluster-cookies som används i Adobe Target 1.x- och 2.x-biblioteken. Med det här alternativet kan du bevara besökarprofilen mellan sidor som använder tidigare Adobe Target-implementeringar och sidor som använder Web SDK.

## Aktivera målmigrering från at.js med hjälp av taggtillägget Web SDK

Markera kryssrutan **[!UICONTROL Migrate Target from at.js to the Web SDK]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Personalization] och markera kryssrutan **[!UICONTROL Migrate Target from at.js to the Web SDK]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Aktivera målmigrering från at.js med Web SDK JavaScript-biblioteket

Ange det booleska värdet `targetMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `false`. Ange det här värdet till `true` om du har sidor som fortfarande använder Adobe Target 1.x- eller 2.x-bibliotek.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```
