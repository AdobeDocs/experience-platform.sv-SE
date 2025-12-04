---
title: idMigrationEnabled
description: Låter Web SDK läsa AMCV-cookies.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

Egenskapen `idMigrationEnabled` gör att Web SDK kan läsa AMCV-cookies som angetts av tidigare Adobe Experience Cloud-implementeringar. Om din organisation uppgraderar din implementering till Web SDK ger den här inställningen en smidigare övergång till den aktuella Adobe Experience Cloud ID-tjänsten. Den här inställningen är värdefull så att du inte ser någon större ökning av antalet unika besökare när du uppgraderar till SDK för webben.

Om din organisation kör en ny implementering av Web SDK påverkar detta inte datainsamling eller besöksidentifiering. Det finns inga nackdelar med att låta det vara aktiverat för alla implementeringar.

Ange det booleska värdet `idMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange den här egenskapen om du vill inaktivera möjligheten att läsa AMCV-cookies som angetts av Visitor API. De flesta organisationer behöver inte ange den här egenskapen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Aktivera migrering av besökar-ID med hjälp av taggtillägget Web SDK

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med hjälp av [inställningarna för identitetskonfiguration](/help/tags/extensions/client/web-sdk/configure/identity.md).
