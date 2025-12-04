---
title: prehideStyle
description: Skapa en CSS-definition som gör att anpassat innehåll kan läsas in utan att det flimrar.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

Med egenskapen `prehidingStyle` kan du definiera en CSS-väljare för att dölja anpassat innehåll tills det läses in. Den här egenskapen är värdefull i synkrona webb-SDK-implementeringar för att undvika flimmer. Adobe rekommenderar att du använder [prehide-fragmentet](/help/collection/use-cases/personalization/manage-flicker.md) för asynkrona Web SDK-implementeringar.

CSS-väljarna som du definierar i den här egenskapen börjar dölja innehåll när du kör det första [`sendEvent`](../sendevent/overview.md)-kommandot på en sida. Innehållet döljs när ett svar från Adobe tas emot, vilket vanligtvis inkluderar personaliserat innehåll. Innehållet döljs också om kommandot `sendEvent` misslyckas eller om timeout uppstår.

Om du inkluderar både `prehidingStyle` och det föregående fragmentet i implementeringen får det föregående fragmentet högre prioritet än den här konfigurationsegenskapen.

Ange strängen `prehidingStyle` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK döljs ingenting när du kör det första `sendEvent`-kommandot på en sida. Ange det här värdet till önskad CSS-väljare och deklarationsblock för synkront inlästa bibliotek.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Dölja format med hjälp av taggtillägget Web SDK

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med hjälp av [Personalization konfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/personalization.md).
