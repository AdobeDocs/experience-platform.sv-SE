---
title: downloadLinkQualifier
description: Hjälper till att avgöra hur automatisk länkspårning kvalificerar nedladdningslänkar.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# `downloadLinkQualifier`

Om du aktiverar automatisk länkspårning med [`clickCollectionEnabled`](clickcollectionenabled.md), `downloadLinkQualifier` -egenskapen hjälper till att fastställa villkoren för att en URL ska betraktas som en nedladdningslänk.

Den här egenskapen är en regex-sträng. Om den klickade URL:en matchar det här regex, `xdm.web.webInteraction.type` är inställd på `"download"`. Länkarna klassificeras också omedelbart som en nedladdningslänk om de innehåller en `download` HTML-attribut. If `clickCollectionEnabled` är inte aktiverat, den här egenskapen gör ingenting.

## Hämta länkkvalificerare med tillägget Web SDK-tagg

Aktivera **[!UICONTROL Enable click data collection]** kryssrutan och sedan ange önskad text under **[!UICONTROL Download link qualifier]** när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Data Collection] markerar du kryssrutan **[!UICONTROL Enable click data collection]**.
1. När den är aktiverad visas **[!UICONTROL Download link qualifier]** visas. Ange önskat värde. Det finns även knappar för att testa regex och återställa standardvärdet.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Hämta länkkvalificerare med JavaScript-biblioteket för Web SDK

Ange `downloadLinkQualifier` sträng när `configure` -kommando. Om du utelämnar den här egenskapen får den som standard följande värde:

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
