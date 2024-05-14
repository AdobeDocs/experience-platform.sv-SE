---
title: data
description: Lär dig hur du skickar data som inte är XDM till Adobe via dataobjektet.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# `data`

The `data` kan du skicka en nyttolast till Adobe som inte matchar ett XDM-schema. Det är användbart i andra scenarier än XDM, som att skicka data direkt till Adobe Analytics, Adobe Target eller Adobe Audience Manager. När data kommer till datastream kan du använda [Förmappning av data](/help/data-prep/ui/mapping.md) för att tilldela XDM-fält till varje fält i `data` -objekt.

>[!IMPORTANT]
>
>Data i det här objektet måste ha minst en av följande åtgärder:
>
>* En tjänst i datastream måste konfigureras för att hämta data från en viss egenskap i `data` -objekt.
>* Den angivna egenskapen måste mappas till ett XDM-fält med hjälp av dataprep.
>
>Om en viss egenskap inte är mappad till ett XDM-fält eller används av en konfigurerad tjänst, går dessa data förlorade permanent.

## Använd `data` objekt via taggtillägget Web SDK {#tag-extension}

Ange ett dataelement i **[!UICONTROL Data]** -fält inom åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-uppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** markerar du önskad regel.
1. Under [!UICONTROL Actions]väljer du en befintlig åtgärd eller skapar en åtgärd.
1. Ange [!UICONTROL Extension] listruta till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange [!UICONTROL Action Type] till **[!UICONTROL Send event]**.
1. Ange det dataelement som innehåller det önskade objektet i **[!UICONTROL Data]** fält.
1. Klicka **[!UICONTROL Keep Changes]** och sedan köra ditt publiceringsarbetsflöde.

## Använd `data` via Web SDK JavaScript-biblioteket {#library}

Ange `data` -objektet som en del av JSON-objektet inom parametern för `sendEvent` -kommando. För data som du planerar att mappa i datastream kan du strukturera det här objektet hur du vill. För data som används av vissa tjänster måste objekthierarkin matcha vad tjänsten förväntar sig. Du kan inkludera båda `data` -objektet och [`xdm`](xdm.md) objekt i samma `sendEvent` -kommando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Använd `data` objekt med Adobe Analytics {#analytics}

Du kan använda `data` med Adobe Analytics för att skicka data till en rapportsserie utan XDM-schema. Variabler är konfigurerade att använda samma syntax som [!DNL AppMeasurement] variabler, förenkla uppgraderingsprocessen till Web SDK. Se [Variabelmappning för dataobjekt till Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) i Adobe Analytics implementeringsguide för mer information.
