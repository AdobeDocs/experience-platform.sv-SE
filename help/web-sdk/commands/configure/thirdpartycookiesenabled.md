---
title: thirdPartyCookiesEnabled
description: Tillåt användning av cookies från tredje part för att identifiera besökare.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

The `thirdPartyCookiesEnabled` egenskapen är ett booleskt värde som avgör om Web SDK anger cookies i en tredjepartskontext. Det här alternativet är användbart om du vill identifiera besökare mellan underdomäner eller domäner som din organisation äger. Många moderna webbläsare begränsar dock inställningen och förfallotiden för cookies från tredje part.

När det här alternativet är aktiverat använder Web SDK Adobe Audience Manager för att identifiera en besökare. När det här alternativet är inaktiverat inaktiveras anropet till Audience Manager. Se [Förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) i användarhandboken för Audience Manager om du vill ha mer information.

## Aktivera cookies från tredje part med taggtillägget Web SDK

Välj **[!UICONTROL Use third-party cookies]** kryssruta när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Identity] markerar du kryssrutan **[!UICONTROL Use third-party cookies]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Aktivera cookies från tredje part med JavaScript-biblioteket för Web SDK

Ange `thirdPartyCookiesEnabled` boolesk när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du inte vill att Web SDK ska använda Audience Manager för att identifiera besökare.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
