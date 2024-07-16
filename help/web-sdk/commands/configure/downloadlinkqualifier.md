---
title: downloadLinkQualifier
description: Hjälper till att avgöra hur automatisk länkspårning kvalificerar nedladdningslänkar.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# `downloadLinkQualifier`

Om du aktiverar automatisk länkspårning med [`clickCollectionEnabled`](clickcollectionenabled.md) hjälper egenskapen `downloadLinkQualifier` till att fastställa villkoren för att en URL ska betraktas som en hämtningslänk.

Den här egenskapen är en regex-sträng. Om den klickade URL:en matchar det här regex, är `xdm.web.webInteraction.type` inställt på `"download"`. Länkarna klassificeras också omedelbart som en nedladdningslänk om de innehåller ett `download` HTML-attribut. Om `clickCollectionEnabled` inte är aktiverat händer ingenting.

## Hämta länkkvalificerare med tillägget Web SDK-tagg

Aktivera kryssrutan **[!UICONTROL Enable click data collection]** och ange sedan önskad text under **[!UICONTROL Download link qualifier]** när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Data Collection] och markera kryssrutan **[!UICONTROL Enable click data collection]**.
1. När textrutan **[!UICONTROL Download link qualifier]** har aktiverats visas den. Ange önskat värde. Det finns även knappar för att testa regex och återställa standardvärdet.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Hämta länkkvalificerare med Web SDK JavaScript-biblioteket

Ange strängen `downloadLinkQualifier` när du kör kommandot `configure`. Om du utelämnar den här egenskapen får den som standard följande värde:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Om du vill använda olika villkor för att kvalificera nedladdningslänkar anger du det här värdet till önskat regex-värde.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
