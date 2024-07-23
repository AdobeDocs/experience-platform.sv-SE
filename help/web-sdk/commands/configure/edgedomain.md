---
title: edgeDomain
description: Avgör den rotdomän som du vill skicka data till.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---

# `edgeDomain`

Med egenskapen `edgeDomain` kan du ändra den domän som Web SDK skickar data till. Den här egenskapen används ofta av organisationer som använder [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). Data skickas till organisationens egen domän, och sedan en CNAME-post vidarebefordrar dessa data till Adobe.

Din organisation fastställer korrekt värde för den här egenskapen när [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) konfigureras. En organisation använder vanligtvis en dedikerad underdomän för detta ändamål. Om du till exempel använder domänen `example.com` kan du konfigurera cookies från första part på `data.example.com`.

## Konfigurera en edge-domän med hjälp av taggtillägget Web SDK

Ange textfältet **[!UICONTROL Edge domain]** när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Leta reda på textfältet **[!UICONTROL Edge domain]** och ange önskat värde.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Konfigurera en edge-domän med hjälp av JavaScript-biblioteket för Web SDK

Ange strängen `edgeDomain` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `edge.adobedc.net`. Ange det här värdet om du vill åsidosätta domänen som Web SDK skickar data till.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```
