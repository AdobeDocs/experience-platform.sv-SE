---
title: orgId
description: Egenskapen orgId är en sträng som talar om för Adobe vilken organisation data skickas till.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# `orgId`

Egenskapen `orgId` är en sträng som talar om för Adobe vilken organisation data skickas till. **Den här egenskapen krävs för alla data som skickas med Web SDK.**

Så här hittar du din `orgID`:

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Tryck **`[Ctrl]`** + **`[I]`** någonstans i Adobe Experience Cloud. Ett [!UICONTROL User Data Debugger]-fönster öppnas.
1. Klicka på **[!UICONTROL Copy]** ![Kopiera](../../assets/copy.png) bredvid [!UICONTROL Current Org ID] eller klicka på fliken **[!UICONTROL Assigned Orgs]** för att visa andra organisation-ID som du har åtkomst till.
1. När du är klar med att hitta den önskade informationen klickar du på **[!UICONTROL Close]**.

Org-ID:n är alltid alfanumeriska strängar med 24 tecken och slutar alltid i `@AdobeOrg`.

## Konfigurera en `orgID` med hjälp av taggtillägget Web SDK

Ange organisations-ID i textfältet **[!UICONTROL IMS organization ID]** när [du konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Ange önskat organisations-ID i textfältet [!UICONTROL IMS organization ID] uppe.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Konfigurera en `orgID` med JavaScript-biblioteket för Web SDK

Ange strängen `orgId` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK genererar Web SDK ett konsolfel och data skickas inte till Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
