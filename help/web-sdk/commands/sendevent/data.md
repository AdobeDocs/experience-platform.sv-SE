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

Med objektet `data` kan du skicka en nyttolast till Adobe som inte matchar ett XDM-schema. Det är användbart i andra scenarier än XDM, som att skicka data direkt till Adobe Analytics, Adobe Target eller Adobe Audience Manager. När data anländer till datastream kan du använda [dataprep-mappning](/help/data-prep/ui/mapping.md) för att tilldela XDM-fält till varje fält i `data`-objektet.

>[!IMPORTANT]
>
>Data i det här objektet måste ha minst en av följande åtgärder:
>
>* En tjänst i datastream måste konfigureras för att hämta data från en angiven egenskap i objektet `data`.
>* Den angivna egenskapen måste mappas till ett XDM-fält med hjälp av dataprep.
>
>Om en viss egenskap inte är mappad till ett XDM-fält eller används av en konfigurerad tjänst, går dessa data förlorade permanent.

## Använd objektet `data` via taggtillägget Web SDK {#tag-extension}

Ange ett dataelement i fältet **[!UICONTROL Data]** i åtgärderna för en taggregel.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Rules]** och markera önskad regel.
1. Välj en befintlig åtgärd under [!UICONTROL Actions] eller skapa en åtgärd.
1. Ställ in listrutefältet [!UICONTROL Extension] på **[!UICONTROL Adobe Experience Platform Web SDK]** och ställ in [!UICONTROL Action Type] på **[!UICONTROL Send event]**.
1. Ange dataelementet som innehåller det önskade objektet i fältet **[!UICONTROL Data]**.
1. Klicka på **[!UICONTROL Keep Changes]** och kör sedan ditt publiceringsarbetsflöde.

## Använd objektet `data` via JavaScript-biblioteket för Web SDK {#library}

Ange objektet `data` som en del av JSON-objektet i parametern för kommandot `sendEvent`. För data som du planerar att mappa i datastream kan du strukturera det här objektet hur du vill. För data som används av vissa tjänster måste objekthierarkin matcha vad tjänsten förväntar sig. Du kan inkludera både objektet `data` och objektet [`xdm`](xdm.md) i samma `sendEvent`-kommando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Använd objektet `data` med Adobe Analytics {#analytics}

Du kan använda objektet `data` med Adobe Analytics för att skicka data till en rapportsvit utan ett XDM-schema. Variabler är konfigurerade att använda samma syntax som [!DNL AppMeasurement]-variabler, vilket förenklar uppgraderingsprocessen till Web SDK. Mer information finns i [Variabelmappning av dataobjekt till Adobe Analytics](https://experienceleague.adobe.com/sv/docs/analytics/implementation/aep-edge/data-var-mapping) i Adobe Analytics implementeringsguide.
