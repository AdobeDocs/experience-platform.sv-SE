---
title: targetMigrationEnabled
description: Tillåt att SDK på webben läser och skriver Adobe Target cookies.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 051374def898d3797711525c5343e0a8454970a2
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# `targetMigrationEnabled`

Egenskapen `targetMigrationEnabled` är en boolesk egenskap som gör att Web SDK kan läsa och skriva de [`mbox` - och `mboxEdgeCluster` cookies &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) som används i Adobe Target 1.x- och 2.x-bibliotek. Med det här alternativet kan du bevara besökarprofilen mellan sidor som använder tidigare Adobe Target-implementeringar och sidor som använder Web SDK.

Ange det booleska värdet `targetMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `false`. Ange det här värdet till `true` om du har sidor som fortfarande använder Adobe Target 1.x- eller 2.x-bibliotek.

När du använder den här egenskapen måste du även aktivera [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) i `targetGlobalSettings()` i din Adobe Target-implementering.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Aktivera målmigrering med hjälp av taggtillägget Web SDK

Den här inställningen kan konfigureras i taggtillägget för Web SDK med hjälp av [Personalization konfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
