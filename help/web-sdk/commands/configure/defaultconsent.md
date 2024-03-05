---
title: defaultConsent
description: Ange standardmetod för insamling av samtycke.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# `defaultConsent`

The `defaultConsent` egenskapen avgör hur du hanterar datainsamlingssamtycke innan du anropar [`setConsent`](../setconsent.md) -kommando. Den här egenskapen är värdefull när du inte av misstag vill samla in data från personer som bor i områden där samtycke krävs innan data samlas in.

Den här egenskapen tillåter tre värden:

* **I**: Datainsamlingen fortsätter som vanligt tills användaren avanmäler sig.
* **Ut**: Data tas bort permanent tills användaren väljer att gå in.
* **Väntande**: Data lagras lokalt tills användaren väljer att använda [`setConsent`](../setconsent.md) -kommando. Data bevaras inte mellan sidinläsningar.

Om du har en besökare som inte omfattas av den allmänna dataskyddsförordningen (GDPR) kan standardsamtycke anges till `in`. Besökare inom GDPR:s jurisdiktion kan få sitt standardsamtycke inställt på `pending`. Din plattform för hantering av samtycke (CMP) kan identifiera kundens region och tillhandahålla flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke.

## Ange standardsamtycke med hjälp av taggtillägget Web SDK

Markera önskad alternativknapp under **[!UICONTROL Default consent]** när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Privacy] väljer du **[!UICONTROL Default consent]**.
1. Klicka **[!UICONTROL Save]** publicera sedan ändringarna.

## Ange standardsamtycke med hjälp av JavaScript-biblioteket för Web SDK

Ange `defaultConsent` strängegenskapen till önskad medgivandenivå när du kör `configure` -kommando. Den här egenskapen är skiftlägeskänslig och stöder endast följande tre värden: `"in"`, `"out"`och `"pending"`. Om du försöker använda något annat värde genereras ett fel i biblioteket.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
