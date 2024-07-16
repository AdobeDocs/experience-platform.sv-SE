---
title: prehideStyle
description: Skapa en CSS-definition som gör att anpassat innehåll kan läsas in utan att det flimrar.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# `prehidingStyle`

Med egenskapen `prehidingStyle` kan du definiera en CSS-väljare för att dölja anpassat innehåll tills det läses in. Den här egenskapen är värdefull i synkrona Web SDK-implementeringar för att undvika flimmer. Adobe rekommenderar att du använder [prehide-fragmentet](../../personalization/manage-flicker.md) för asynkrona Web SDK-implementeringar.

CSS-väljarna som du definierar i den här egenskapen börjar dölja innehåll när du kör det första [`sendEvent`](../sendevent/overview.md)-kommandot på en sida. Innehållet döljs när ett svar från Adobe tas emot, vilket vanligtvis inkluderar personaliserat innehåll. Innehållet döljs också om kommandot `sendEvent` misslyckas eller om timeout uppstår.

Om du inkluderar både `prehidingStyle` och det föregående fragmentet i implementeringen får det föregående fragmentet högre prioritet än den här konfigurationsegenskapen.

## Dölja format med tillägget Web SDK-tagg

Klicka på knappen **[!UICONTROL Provide prehiding style]** när du [konfigurerar taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Personalization] och markera sedan knappen **[!UICONTROL Provide prehiding style]**.
1. Den här knappen öppnar ett modalt fönster med en CSS-redigerare. Infoga önskad CSS-väljare och deklarationsblock och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka på **[!UICONTROL Save]** under tilläggsinställningarna och publicera sedan ändringarna.

## Dölja format med hjälp av JavaScript-biblioteket för Web SDK

Ange strängen `prehidingStyle` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK döljs ingenting när du kör det första `sendEvent`-kommandot på en sida. Ange det här värdet till önskad CSS-väljare och deklarationsblock för synkront inlästa bibliotek.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
