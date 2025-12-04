---
title: downloadLinkQualifier
description: Hjälper till att avgöra hur automatisk länkspårning kvalificerar nedladdningslänkar.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Om du aktiverar automatisk länkspårning med [`clickCollectionEnabled`](clickcollectionenabled.md) hjälper egenskapen `downloadLinkQualifier` till att fastställa villkoren för att en URL ska betraktas som en hämtningslänk.

Den här egenskapen är en regex-sträng. Om den klickade URL:en matchar det här regex, är `xdm.web.webInteraction.type` inställt på `"download"`. Länkarna klassificeras också omedelbart som en nedladdningslänk om de innehåller ett `download` HTML-attribut. Om `clickCollectionEnabled` inte är aktiverat händer ingenting.

Ange strängen `downloadLinkQualifier` när du kör kommandot `configure`. Om du utelämnar den här egenskapen får den som standard följande värde:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Om du vill använda olika villkor för att kvalificera nedladdningslänkar anger du det här värdet till önskat regex-värde.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Ladda ned länkkvalificerare med taggtillägget Web SDK

SDK-taggtilläggets motsvarighet för det här fältet finns under [Konfigurationsinställningar för datainsamling](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier) när du konfigurerar taggtillägget.
