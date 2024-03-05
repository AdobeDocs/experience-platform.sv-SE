---
title: edgeDomain
description: Avgör den rotdomän som du vill skicka data till.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 1%

---

# `edgeDomain`

The `edgeDomain` kan du ändra domänen där Web SDK skickar data. Den här egenskapen används ofta av organisationer som använder [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). Data skickas till organisationens egen domän, och sedan en CNAME-post vidarebefordrar dessa data till Adobe.

Organisationen bestämmer korrekt värde för den här egenskapen vid konfiguration [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html). En organisation använder vanligtvis en dedikerad underdomän för detta ändamål. Om du till exempel använder domänen `example.com`kan du konfigurera cookies från första part på `data.example.com`.

## Konfigurera en edge-domän med hjälp av taggtillägget Web SDK

Ange **[!UICONTROL Edge domain]** textfält när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Hitta textfältet **[!UICONTROL Edge domain]** anger du önskat värde.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Konfigurera en edge-domän med JavaScript-biblioteket för Web SDK

Ange `edgeDomain` sträng när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar SDK blir standardvärdet `edge.adobedc.net`. Ange det här värdet om du vill åsidosätta domänen som Web SDK skickar data till.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeDomain": "data.example.com"
});
```
