---
title: targetMigrationEnabled
description: Tillåt att SDK på webben läser och skriver Adobe Target cookies.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: dade74bf4a5cfd7b60eaf216583deb67b93a61db
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# `targetMigrationEnabled`

Egenskapen `targetMigrationEnabled` är en boolesk egenskap som gör att Web SDK kan läsa och skriva de [`mbox` - och `mboxEdgeCluster` cookies &#x200B;](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk) som används i Adobe Target 1.x- och 2.x-bibliotek. Med det här alternativet kan du bevara besökarprofilen mellan sidor som använder tidigare Adobe Target-implementeringar och sidor som använder Web SDK.

Ange det booleska värdet `targetMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `false`. Ange det här värdet till `true` om du har sidor som fortfarande använder Adobe Target 1.x- eller 2.x-bibliotek.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Aktivera målmigrering med hjälp av taggtillägget Web SDK

Den här inställningen kan konfigureras i taggtillägget för Web SDK med hjälp av [Personalization konfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
