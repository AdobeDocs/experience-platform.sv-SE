---
title: thirdPartyCookiesEnabled
description: Tillåt användning av cookies från tredje part för att identifiera besökare.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [har meddelat](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) att Chrome-stöd för cookies från tredje part kommer att upphöra under andra halvåret 2024. Detta innebär att cookies från tredje part inte längre stöds i någon av de större webbläsarna.
>
>När den här ändringen implementeras upphör Adobe stödet för den `demdex`-cookie som för närvarande stöds i Web SDK.


Egenskapen `thirdPartyCookiesEnabled` är en boolesk egenskap som avgör om Web SDK anger cookies i en tredjepartskontext. Det här alternativet är användbart om du vill identifiera besökare mellan underdomäner eller domäner som din organisation äger. Många moderna webbläsare begränsar dock inställningen och förfallotiden för cookies från tredje part.

När det här alternativet är aktiverat använder Web SDK Adobe Audience Manager för att identifiera en besökare. När det här alternativet är inaktiverat inaktiveras anropet till Audience Manager. Mer information finns i [Förstå anrop till Demdex-domänen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html) i användarhandboken för Audience Manager.

## Aktivera cookies från tredje part med taggtillägget Web SDK

Markera kryssrutan **[!UICONTROL Use third-party cookies]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Identity] och markera kryssrutan **[!UICONTROL Use third-party cookies]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Aktivera cookies från tredje part med hjälp av Web SDK JavaScript-biblioteket

Ange det booleska värdet `thirdPartyCookiesEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange det här värdet till `false` om du inte vill att Web SDK ska använda Audience Manager för att identifiera besökare.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
