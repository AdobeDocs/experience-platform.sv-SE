---
title: orgId
description: Egenskapen orgId är en sträng som talar om för Adobe vilken organisation data skickas till.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# `orgId`

The `orgId` -egenskapen är en sträng som talar om för Adobe vilken organisation data skickas till. **Den här egenskapen krävs för alla data som skickas med Web SDK.**

Hitta dina `orgID`:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Var som helst inom Adobe Experience Cloud, tryck **`[Ctrl]`** + **`[I]`**. A [!UICONTROL User Data Debugger] öppnas.
1. Klicka **[!UICONTROL Copy]** ![Kopiera](../../assets/copy.png) bredvid [!UICONTROL Current Org ID]eller klicka på **[!UICONTROL Assigned Orgs]** om du vill visa andra organisations-ID:n som du har åtkomst till.
1. När du är klar med att hitta den önskade informationen klickar du på **[!UICONTROL Close]**.

Org-ID:n är alltid alfanumeriska strängar med 24 tecken och avslutas alltid med `@AdobeOrg`.

## Konfigurera en `orgID` med taggtillägget Web SDK

Ange organisation-ID i dialogrutan **[!UICONTROL IMS organization ID]** textfält när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Ange önskat organisations-ID i [!UICONTROL IMS organization ID] textfält nära överkanten.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Konfigurera en `orgID` med Web SDK JavaScript-biblioteket

Ange `orgId` sträng när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK genererar Web SDK ett konsolfel och data skickas inte till Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
