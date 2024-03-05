---
title: prehideStyle
description: Skapa en CSS-definition som gör att anpassat innehåll kan läsas in utan att det flimrar.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# `prehidingStyle`

The `prehidingStyle` Med -egenskapen kan du definiera en CSS-väljare för att dölja anpassat innehåll tills det läses in. Den här egenskapen är värdefull i synkrona Web SDK-implementeringar för att undvika flimmer. Adobe rekommenderar att du använder [dölja fragment](../../personalization/manage-flicker.md) för asynkrona Web SDK-implementeringar.

CSS-väljarna som du definierar i den här egenskapen börjar dölja innehåll när du kör den första [`sendEvent`](../sendevent/overview.md) på en sida. Innehållet döljs när ett svar från Adobe tas emot, vilket vanligtvis inkluderar personaliserat innehåll. Innehållet döljs också om `sendEvent` kommandot misslyckas eller timeout inträffar.

Om du inkluderar båda `prehidingStyle` och det föregående dolda fragmentet i implementeringen, prioriterar det föregående dolda fragmentet framför den här konfigurationsegenskapen.

## Dölja format med tillägget Web SDK-tagg

Välj **[!UICONTROL Provide prehiding style]** knapp när [konfigurera taggtillägget](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och sedan klicka **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK] kort.
1. Bläddra nedåt till [!UICONTROL Personalization] markerar du knappen **[!UICONTROL Provide prehiding style]**.
1. Den här knappen öppnar ett modalt fönster med en CSS-redigerare. Infoga önskad CSS-väljare och deklarationsblock och klicka sedan på **[!UICONTROL Save]** för att stänga det modala fönstret.
1. Klicka **[!UICONTROL Save]** publicera ändringarna under tilläggsinställningarna.

## Dölja format med JavaScript-biblioteket för Web SDK

Ange `prehidingStyle` sträng när `configure` -kommando. Om du utelämnar den här egenskapen när du konfigurerar Web SDK döljs ingenting när du kör den första `sendEvent` på en sida. Ange det här värdet till önskad CSS-väljare och deklarationsblock för synkront inlästa bibliotek.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
