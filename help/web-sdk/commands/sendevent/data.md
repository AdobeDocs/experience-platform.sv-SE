---
title: data
description: Lär dig hur du skickar data som inte är XDM till Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# data

The `data` kan du skicka data till Adobe som inte matchar ett XDM-schema. Det är användbart i andra scenarier än XDM, som att uppdatera en [Adobe Target](/help/web-sdk/personalization/adobe-target/target-overview.md). När data kommer till Adobe kan du använda datastream-mappningsverktyget för att tilldela XDM-fält till varje fält i `data` -egenskap.

>[!IMPORTANT]
>
>Data i den här egenskapen måste ha minst en av följande åtgärder:
>
>* En tjänst i datastream måste konfigureras för att hämta data från en specifik egenskap i `data` object
>* Varje egenskap måste mappas till ett XDM-fält
>
>Om ett givet fält inte är mappat till ett XDM-fält eller används av en konfigurerad tjänst, går dessa data förlorade permanent.

## Använd egenskapen data med hjälp av taggtillägget Web SDK

Ange ett dataelement i **[!UICONTROL Data]** -fält inom åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Ange det dataelement som innehåller det önskade objektet i **[!UICONTROL Data]** fält.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Använda egenskapen data med JavaScript-biblioteket för Web SDK

Ange `data` som en del av JSON-objektet inom parametern för `sendEvent` -kommando. För data som du planerar att mappa i datastream kan du strukturera den här egenskapen hur du vill. För data som används av vissa tjänster måste objekthierarkin matcha vad tjänsten förväntar sig. Du kan inkludera båda `data` -objektet och [`xdm`](xdm.md) objekt i samma `sendEvent` -kommando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
