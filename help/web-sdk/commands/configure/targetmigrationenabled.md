---
title: targetMigrationEnabled
description: Tillåt att Web SDK läser och skriver Adobe Target-cookies.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# `targetMigrationEnabled`

The `targetMigrationEnabled` egenskapen är en boolesk funktion som gör att Web SDK kan läsa och skriva de mbox- och mboxEdgeCluster-cookies som används i Adobe Target 1.x- och 2.x-biblioteken. Med det här alternativet kan du bevara besökarprofilen mellan sidor som använder tidigare Adobe Target-implementeringar och sidor som använder Web SDK.

## Aktivera målmigrering från at.js med hjälp av taggtillägget Web SDK

Välj **[!UICONTROL Migrate Target from at.js to the Web SDK]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Personalization] markerar du kryssrutan **[!UICONTROL Migrate Target from at.js to the Web SDK]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Aktivera målmigrering från at.js med JavaScript-biblioteket för Web SDK

Ange `targetMigrationEnabled` boolesk när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `false`. Ange det här värdet till `true` om du har sidor som fortfarande använder Adobe Target 1.x- eller 2.x-biblioteken.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
